# Valid Palindrome II

**題目：**

[https://leetcode.com/problems/valid-palindrome-ii/](https://leetcode.com/problems/valid-palindrome-ii/)

題意：

最多能刪除一個字元，並判斷字串是否能成為迴文。

**解法：**

按照原本Valid Palindrome的作法，但比較時，每次skip掉一個字元，不過此法複雜度高，會超時。

```java
class Solution {
    public boolean validPalindrome(String s) {
        if (isPalindrome(s, Integer.MAX_VALUE)) {
            return true;
        }

        for (int i = 0; i < s.length(); i++) {
            if (isPalindrome(s, i)) {
                return true;
            }
        }

        return false;
    }

    public boolean isPalindrome(String s, int pos) {
        if (s.length() < 2) {
            return true;
        }

        int start = 0;
        int end = s.length() - 1;
        while (start <= end) {
            while (start < s.length() && (!Character.isLetterOrDigit(s.charAt(start)) || start == pos)) {
                start++;
            }

            while (end > 0 && (!Character.isLetterOrDigit(s.charAt(end)) || end == pos)) {
                end--;
            }

            if (start <= end && Character.toLowerCase(s.charAt(start)) != Character.toLowerCase(s.charAt(end))) {
                return false;
            }
            start++;
            end--;
        }

        return true;
    }
}
```

看了花花大神的講解，我們可以用以下方法來簡化，依舊還是照兩端指針不斷比較，一但比較到string\[L\] != string\[R\] 時，我們比例再去驗證中間那段是否為迴文，有以下兩個選項可驗證

* isPalindrome\(s, L + 1, R\)，驗證去掉string\(L\)那個字元後，中間那段文字是否為迴文。

* isPalindrome\(s, L, R + 1\)，驗證去掉string\(R\)那個字元後，中間那段文字是否為迴文。

```java
class Solution {
    public boolean validPalindrome(String s) {
        
        int start = 0;
        int end = s.length() - 1;
        while (start < end) {
            if (s.charAt(start) != s.charAt(end)) {
                return isPalindrome(s, start + 1, end) || isPalindrome(s, start, end - 1);
            } else {
                start++;
                end--;
            }
        }
        
        return true;
    }
    
    public boolean isPalindrome(String s, int left, int right) {
        if (s.length() < 2) {
            return true;
        }
        
        int start = left;
        int end = right;
        
        while (start <= end) {
            while (start < s.length() && !Character.isLetterOrDigit(s.charAt(start))) {
                start++;
            }
            
            while (end > 0 && !Character.isLetterOrDigit(s.charAt(end))) {
                end--;
            }
            
            
            if (start <= end && Character.toLowerCase(s.charAt(start)) != Character.toLowerCase(s.charAt(end))) {
                return false;
            }
            start++;
            end--;
        }
        
        return true;
        
    }
}
```

**Reference:**

* [https://www.youtube.com/watch?v=hvI-rJyG4ik&t=62s](https://www.youtube.com/watch?v=hvI-rJyG4ik&t=62s)



