#Anagrams

[原題網址](http://www.lintcode.com/en/problem/anagrams/)

解題思路：利用 Compare String 的那個程式，去跟陣列中的每個字串作比較，為了不作太多不必要的運算，在此使用了 hasAnagram 陣列，只要之有找到可搭配的 anagram 則把該位置設為真，一但遇到為真，則把該字串加入結果裡。

```java
public class Solution {
    /**
     * @param strs: A list of strings
     * @return: A list of strings
     */
    public List<String> anagrams(String[] strs) {
        
        List<String> res = new ArrayList<String>();
        boolean[] hasAnagram = new boolean[strs.length];
        
        if (strs.length == 0) {
            return res;
        }
        
        for (int i = 0; i < strs.length; i++) {
            if (hasAnagram[i]) {
                res.add(strs[i]);
                continue;
            }
            for (int j = i + 1; j < strs.length; j++) {
                if (isAnagram(strs[i], strs[j])) {
                    hasAnagram[i] = true;
                    hasAnagram[j] = true;
                    if (!res.contains(strs[i])) {
                        res.add(strs[i]);
                    }
                }
            }
        }
        
        return res;
    }
    
    private boolean isAnagram(String s, String t) {
        
        if (s.length() != t.length()) {
            return false;
        }
        
        int[] map = new int[256];
        for (int i = 0; i < s.length(); i++) {
            map[s.charAt(i) - 'a']++;
            map[t.charAt(i) - 'a']--;
        }
        
        for (int i = 0; i < 256; i++) {
            if (map[i] != 0) {
                return false;
            }
        }
        
        return true;
    }
}

```
>Time Complexity：O(n)