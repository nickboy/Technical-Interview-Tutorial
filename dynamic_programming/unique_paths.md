# Unique Paths

[Leetcode](https://leetcode.com/problems/unique-paths/)

題意：


解題思路：

使用一維陣列的dp來解

```java
public class Solution {
    public int uniquePaths(int m, int n) {
        if (m < 0 || n < 0) {
            return 0;
        }
        
        int[] res = new int[n];
        res[0] = 1;
        for (int i = 0; i < m; i++) {
            for (int j = 1; j < n; j++) {
                res[j] += res[j - 1];
            }
        }
        
        return res[n - 1];
    }
}
```