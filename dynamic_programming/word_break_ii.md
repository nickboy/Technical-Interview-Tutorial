# Word Break II

[Leetcode](https://leetcode.com/problems/word-break-ii/)

題意：

Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

Return all such possible sentences.

For example, given
s = "catsanddog",
dict = ["cat", "cats", "and", "sand", "dog"].

A solution is ["cats and dog", "cat sand dog"].


解題思路：

使用暴力法解，每次加一個字元來判斷是否在字典裡，若是，則繼續往下遞迴，否則就結束。

但此法 leetcode會超時

```java
public class Solution {
    List<String> res = new ArrayList<String>();
    public List<String> wordBreak(String s, Set<String> wordDict) {
        if (s == null || wordDict == null || wordDict.size() == 0) {
            return res;
        }
        helper(s, wordDict, new String(), 0);
        return res;
    }
    
    private void helper(String s, Set<String> wordDict, String temp, int start) {
        if (start >= s.length()) {
            res.add(temp);
            return;
        }
        
        StringBuilder sb = new StringBuilder();
        for (int i = start; i < s.length(); i++) {
            sb.append(s.charAt(i));
            if (wordDict.contains(sb.toString())) {
                if (temp.length() == 0) {
                    temp = sb.toString();
                } else {
                    temp = temp + " " + sb.toString();
                }
                helper(s, wordDict, temp, i + 1);
            }
        }
    }
}
```
---
###Reference
1. http://blog.csdn.net/linhuanmars/article/details/22452163