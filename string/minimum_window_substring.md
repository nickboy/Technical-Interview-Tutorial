#Minimum Window Substring

[原題網址](http://www.lintcode.com/en/problem/minimum-window-substring/)

題意：給定source 與target兩個字串，找出source最短的子字串包含target所有的字串。

解題思路：使用兩個陣列分別記錄 source 與 target 的字符個數，其中 source 只紀錄 i 到 j 之間的字符個數。

```java
public class Solution {
    /**
     * @param source: A string
     * @param target: A string
     * @return: A string denote the minimum window
     *          Return "" if there is no such a string
     */
    public String minWindow(String source, String target) {
        
        if (source == null || source.length() == 0 || target == null || target.length() == 0) {
            return "";
        }
        

        int[] sourceHash = new int[256];
        int[] targetHash = new int[256];
        
        for (int i = 0; i < target.length(); i++) {
            targetHash[target.charAt(i)] += 1;
        }
        
        int length = Integer.MAX_VALUE;
        int[] idx = new int[2];
        idx[0] = -1;
        idx[1] = -1;
        
        for (int i = 0, j = 0; i < source.length(); i++) {
            while (j < source.length() && !valid(sourceHash, targetHash)) {
                sourceHash[source.charAt(j)] += 1;
                j++;
            }
            if (valid(sourceHash, targetHash)) {
                if (length > j - i) {
                    idx[0] = i;
                    idx[1] = j;
                    length = j - i;
                }
            }
            sourceHash[source.charAt(i)] -= 1;
        }
        
        if (idx[0] == -1 && idx[1] == -1) {
            return "";
        } else {
            return source.substring(idx[0], idx[1]);
        }
        
    }
    
    private boolean valid(int[] sourceHash, int[] targetHash) {
        
        for (int i = 0; i < targetHash.length; i++) {
            if (targetHash[i] > 0 && sourceHash[i] < targetHash[i]) {
                return false;
            }
        }
        
        return true;
    }
}

```