# K Sum

[Lintcode](http://www.lintcode.com/en/problem/k-sum/)

題意：

Given n distinct positive integers, integer k (k <= n) and a number target.

Find k numbers where sum is target. Calculate how many solutions there are?

Example

Given [1,2,3,4], k = 2, target = 5.

There are 2 solutions: [1,4] and [2,3].

Return 2.

解題思路：

網友[Yu Zhang](http://www.cnblogs.com/yuzhangcmu/p/4279676.html) 與九章提供以下思路：

動規法：

>f[i][j][t] 表示前i個數中，選出j個數，組成 sum為 t 有多少種方案. 

>f[i][j][t] = f[i - 1][j - 1][t - A[i]] + f[i - 1][j][t]

上面遞迴式分為兩個部份

* f[i - 1][j - 1][t - A[i]]，表示考慮當前 A[i - 1]這個數，所以只要從前i - 1個數中挑j - 1個數，組合成 t - A[i] 即可。
* f[i - 1][j][t]，表示不選 A[i - 1] 這個數，所以就是從前面i - 1個數中直接挑 j 個。


其程式碼如下：

```java
public class Solution {
    /**
     * @param A: an integer array.
     * @param k: a positive integer (k <= length(A))
     * @param target: a integer
     * @return an integer
     */
    public int kSum(int A[], int k, int target) {
        if (A == null || A.length == 0 || k == 0) {
            return 0;
        }
        
        int len = A.length;
        int[][][] dp = new int[len + 1][k + 1][target + 1];
        
        for (int i = 0; i <= len; i++) {
            for (int j = 0; j <= k; j++) {
                for (int t = 0; t <= target; t++) {
                    if (j == 0 && t == 0) {
                        // 表示從前i個數中選0個數使得target 等於0的方案數為多少
                        // 因為不選半個，sum為0 且target也為0 ，則方案為一種
                        dp[i][j][t] = 1;
                    } else if (!((i == 0) || (j == 0) || (t == 0))) {
                        dp[i][j][t] = dp[i - 1][j][t];
                        // 要確保非負數，因為我們要拿這個來當作index
                        if ((t - A[i - 1]) >= 0) {
                            dp[i][j][t] += dp[i - 1][j - 1][t - A[i - 1]];
                        }
                    }
                }
            }
        }
        
        return dp[len][k][target];
    }
}
```


---
###Reference

1. http://www.cnblogs.com/yuzhangcmu/p/4279676.html