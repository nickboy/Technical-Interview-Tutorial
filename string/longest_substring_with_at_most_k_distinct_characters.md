#Longest Substring with at Most k Distinct Characters

[原題網址](http://www.lintcode.com/en/problem/longest-substring-with-at-most-k-distinct-characters/)

解題思路：與Minimum Window Substring類似，但此解法只過了四個case，日後找到bug後再來修正。
```java
public int lengthOfLongestSubstringKDistinct(String s, int k) {
        
    if (s == null || s.length() == 0 || k == 0) {
        return 0;
    }
    
    int maxLength = 0;
    HashMap<Character, Integer> map = new HashMap<Character, Integer>();

    for (int i = 0, j = 0; i < s.length(); i++) {
        
        while (j < s.length() && map.size() < k) {
            
            char cur = s.charAt(j);
            if (map.containsKey(cur)) {
                map.put(cur, map.get(cur) + 1);
            } else {
                map.put(cur, 1);
            }
            j++;
        } 
        
        if (map.size() <= k) {
            maxLength = Math.max(maxLength, j - i);    
        }
        
        char charToBeDelete =  s.charAt(i);
        if (map.get(charToBeDelete) > 1) {
            map.put(charToBeDelete, map.get(charToBeDelete) - 1);
        } else {
            map.remove(charToBeDelete);
        }
    }
    
    return maxLength;
}
```