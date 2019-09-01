# Valid Palindrome II

題目：

[https://leetcode.com/problems/valid-palindrome-ii/](https://leetcode.com/problems/valid-palindrome-ii/)

題意：

最多能刪除一個字元，並判斷是否能成為Palindrome。



解法：

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



