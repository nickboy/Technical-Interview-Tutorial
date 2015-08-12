#Palindrome Partition II

[原題網址](http://www.lintcode.com/en/problem/palindrome-partitioning-ii/)

解題思路：
+ f[i] 表示的是 j + 1 到I是回文串，因可能有多個 j ，所以取最少的刀數再加一。
+ 初始化f[i] = i - 1 (f[0] = -1) 是說明從0到i，最差的情況，每隔一個char切一刀也能成為迴文串，之後演算法要試著去降低這刀數。
+ 因程式需要判斷substring是否為迴文，如果判所是否迴文這段若不用陣列之前算過的結果的話，每次都要花O(k)，k為substring的長度，來算。時間複雜度會到達 O(N^3)

```java

public class Solution {
    /**
     * @param s a string
     * @return an integer
     */
    public int minCut(String s) {
        // write your code here
        if (s == null || s.length() == 0) {
            return 0;
        }
        //初始化，極端的情況下就是每隔一個char就切一刀
        //設為lenght+1，是因為要紀錄前i個char最小需要切幾刀
        //預設f[0] = -1
        int[] res = new int[s.length() + 1];
        for (int i = 0; i <= s.length(); i++) {
            res[i] = i - 1;
        }
        
        //主程式
        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (isPalindrome(s, j , i - 1)) {
                    res[i] = Math.min(res[i], res[j] + 1);
                }
            }
        }
        return res[s.length()];
    }
    
    private boolean isPalindrome(String s, int start, int end) {
        while (start < end) {
            if (s.charAt(start) != s.charAt(end)) {
                return false;
            }
            start++;
            end--;
        }
        return true;
    }
}
```
