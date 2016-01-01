# Generalized Abbreviation

[Leetcode](https://leetcode.com/problems/generalized-abbreviation/)

題意：

Write a function to generate the generalized abbreviations of a word.

Example:
Given word = "word", return the following list (order does not matter):
```java
["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]
```

解題思路：

一樣類似subset那樣用backtracking來作，每個字元可以分成兩個情況：

1. 保留：則直接把該字元加入當下的tempRes，繼續往下遞迴
2. 縮寫：count加1，且不加入該字元，繼續往下遞迴


>最後要加入時，要記得檢查count是否大於0，若是的話，要補上再加到res

```java
public class Solution {
    public List<String> generateAbbreviations(String word) {
        List<String> res = new ArrayList<>();
        helper(word, 0, "", 0, res);
        return res;
    }
    
    private void helper(String word, int pos, String tempRes, int count, List<String> res) {
        if (pos == word.length()) {
            if (count > 0) {
                tempRes += count;
            }
            res.add(tempRes);
            return;
        } else {
            
            // keep accumulate the number with add new char to tempRes
            helper(word, pos + 1, tempRes, count + 1, res);
            
            String str = tempRes + ((count > 0) ? count : "") + word.charAt(pos); 
            helper(word, pos + 1, str, 0, res);
        }
        
        
    }
}
```


---
###Reference
1. https://leetcode.com/discuss/75754/java-backtracking-solution