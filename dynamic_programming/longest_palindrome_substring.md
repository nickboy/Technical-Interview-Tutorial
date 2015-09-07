#Longest Palindrome Substring

[原題網址](http://www.lintcode.com/en/problem/longest-palindromic-substring/)

題意：從字串 S 中找出最長的迴文

Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

**Example**

Given the string = "abcdzdcab", return "cdzdc".

**Challenge**

O(n2) time is acceptable. Can you do it in O(n) time.

解題思路：可以使用動態規劃來幫助我們解決這道問題，

$$O(N^{2})$$解法：枚舉子字串的起始點與終點，dp[i][j]代表從字串取出 i 到 j 的子字串是否為迴文，可以透過比較第i個字元是否與第j個字元相同，並且兩者之間的子字串是否為迴文。

>```dp[i][j] = (s.charAt(i) == s.charAt(j)) && dp[i + 1][j - 1]```

原始碼如下：

```java
public String longestPalindrome(String s) {
    
    if (s == null || s.length() < 2) {
        return s;
    }
    
    int len = s.length();
    boolean[][] dp = new boolean[len][len];
    String res = "";
    int maxLength = 0;
    
    // j枚舉終點，i枚舉超始點
    // subString(i,j)表示從string的index i取到j-1，即不包含j本身。
    for (int j = 0; j < len; j++) {
        for (int i = 0; i <= j; i++) {
            
            dp[i][j] = (s.charAt(i) == s.charAt(j)) && ( j - i < 2 || dp[i+1][j-1]);
            
            if (dp[i][j]) {
                if (j - i + 1 > maxLength) {
                    maxLength = j - i + 1;
                    res = s.substring(i, j + 1);
                }
            }
        }
    }
    
    return res;
}
```
---
$$O(N)$$解法：待補完


---
###Reference
1. http://www.cnblogs.com/yuzhangcmu/p/4189068.html
2. http://blog.csdn.net/hopeztm/article/details/7932245
