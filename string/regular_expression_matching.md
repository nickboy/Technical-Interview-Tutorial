# Regular Expression Matching

[Leetcode](https://leetcode.com/problems/regular-expression-matching/)

題意：

Implement regular expression matching with support for '.' and '*'.

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```


解題思路：

網友 [Simple and Stupid](http://simpleandstupid.com/2014/10/14/regular-expression-matching-leetcode-%E8%A7%A3%E9%A2%98%E7%AC%94%E8%AE%B0/) 提供了以下思路：

"主要思路是遞歸，每次比較s和p的第一個字符，難點主要集中在對 \* 的處理，幾種分支情況要想清楚。
主要有兩個case：
1. p的第二個字符不是 \* ，這種是簡單情況。
2. p的第二個字符是 \*，這種情況相對複雜。

對於每次對比，還要注意p的第一個字符是否為 .，如果是，則match，繼續比較後面的。
"

---
###Reference
1. http://simpleandstupid.com/2014/10/14/regular-expression-matching-leetcode-%E8%A7%A3%E9%A2%98%E7%AC%94%E8%AE%B0/
2. 