#Longest Common Prefix

[原題網址](http://www.lintcode.com/en/problem/longest-common-prefix/)

題意：給予一個字串陣列，找出最長的共同 prefix。

解題思路：拿第一個字串的第 i 個字元與陣列中其他所有元素的第 i 個字元相比，若都相同，則進行第 i + 1 個字元的比對，若不同，則返回當前的最優解，為了避免耗費太多比對動作，與 out of bound 錯誤，我們必須找出最短的字串長度，其程式碼如下：

```java
public String longestCommonPrefix(String[] strs) {
    
    if (strs == null || strs.length == 0) {
        return "";
    }
    
    int shortestLength = Integer.MAX_VALUE;
    for (int i = 0; i < strs.length; i++) {
        if (strs[i].length() < shortestLength) {
            shortestLength = strs[i].length();
        }
    }
    
    String res = "";
    for (int i = 0; i < shortestLength; i++) {
        char c = strs[0].charAt(i);
        for (int j = 1; j < strs.length; j++) {
            if (c != strs[j].charAt(i)) {
                return res;
            }
        }
        
        res = strs[0].substring(0, i + 1);
    }
    
    return res;
}
```


找到一個更簡潔的方法，拿第一個字串當作prefix，不斷的去與剩下的字串比較，只要```strs[idx].indexOf(prefix) != 0```(代表找不到或是index不在啟始位置)，則不斷縮短prefix。

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }
        
        String prefix = strs[0];
        int idx = 1;
        
        while (idx < strs.length) {
            
            while (strs[idx].indexOf(prefix) != 0) {
                prefix = prefix.substring(0, prefix.length() - 1);
            }
            idx++;
        }
        
        return prefix;
    }
}
```

來源：[Medium link](https://medium.com/@desolution/從leetcode學演算法-2-d4189f53018e)
