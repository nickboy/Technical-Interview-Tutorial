# Maximum Product of Word Lengths

[Leetcode](https://leetcode.com/problems/maximum-product-of-word-lengths/)

題意：

Given a string array words, find the maximum value of length(word[i]) * length(word[j]) where the two words do not share common letters. You may assume that each word will contain only lower case letters. If no such two words exist, return 0.

Example 1:
Given ["abcw", "baz", "foo", "bar", "xtfn", "abcdef"]
Return 16
The two words can be "abcw", "xtfn".

Example 2:
Given ["a", "ab", "abc", "d", "cd", "bcd", "abcd"]
Return 4
The two words can be "ab", "cd".

Example 3:
Given ["a", "aa", "aaa", "aaaa"]
Return 0
No such pair of words.



解題思路：

不斷的拿一個字與後面的所有字來作比較，用一個陣列來紀錄當前的字有哪些字母，一但遇到有相同的字母則直接跳出，否則計算出兩個字串的長度乘積是否與目前max還大。


```java
public class Solution {
    public int maxProduct(String[] words) {
        if (words == null || words.length == 0) {
            return 0;
        }
        
        int res = 0;
        for (int i = 0; i < words.length; i++) {
            int[] letters = new int[26];
            for (char c : words[i].toCharArray()) {
                letters[c - 'a']++;
            }
            
            for (int j = i + 1; j < words.length; j++) {
                int k = 0;
                for (;k < words[j].length(); k++) {
                    if (letters[words[j].charAt(k) - 'a'] != 0) {
                        break;
                    }
                }
                if (k == words[j].length()) {
                    res = Math.max(res, words[i].length() * words[j].length());
                }
            }
        }
        
        return res;
    }
}
```