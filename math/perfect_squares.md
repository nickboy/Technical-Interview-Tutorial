# Perfect Squares

[Leetcode](https://leetcode.com/problems/perfect-squares/)

題意：

Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

For example, given n = 12, return 3 because 12 = 4 + 4 + 4; given n = 13, return 2 because 13 = 4 + 9.


解題思路：

遞迴法，複雜度相當高

```java
public class Solution {
    public int numSquares(int n) {
        int res = n;
        int num = 2;
        
        while(num * num <= n) {
            int a = n / (num * num);
            int b = n % (num * num);
            res = Math.min(res, a + numSquares(b));
            num++;
        }
        return res;
    }
}
```
DP法：

DP[i] 表示能形成 i 的最少perfect squares，遞迴式如下：

>dp[i + j \* j] = Math.min(dp[i + j * j], dp[i] + 1)

>dp[i] + 1 表示只需要最少算出 i 的完美平方數，再加上j*j即可。

```java
public class Solution {
    public int numSquares(int n) {
        if (n < 2) {
            return 1;
        }
        
        
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        for (int i = 0; i * i <= n; i++) {
            dp[i * i] = 1;
        }
        
        for (int i = 0; i <= n; i++) {
            for (int j = 1; i + j * j <= n; j++) {
                // dp[i] + 1 表示只需要最少算出i的數，再加上j*j即可。
                dp[i + j * j] = Math.min(dp[i + j * j], dp[i] + 1);
            }
        }
        
        return dp[n];
    }
}
```



---
###Reference
1. http://www.cnblogs.com/grandyang/p/4800552.html