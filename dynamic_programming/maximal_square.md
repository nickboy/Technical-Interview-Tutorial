#Maximal Square

[]()

題意：

Given an array of integers and a number k, find k non-overlapping subarrays which have the largest sum.

The number in each subarray should be contiguous.

Return the largest sum.

**Example**

Given $$[-1,4,-2,3,-2,3]$$, $$k=2$$, return $$8$$

**Note**

The subarray should contain at least one number

解題思路：

暴力法：枚舉陣列中的每個元素當矩型的左上元素，不斷的向右下延伸，時間複雜度約為 $$O(N^{6})$$

動態規劃法： dp[i][j] 代表以 i 與 J 作為正方形右下角可以拓展的最大邊長，即找出相鄰的三個元素(左上，上，左)中能延伸的最短長度再加一，時間複雜度約為 $$O(N^{2})$$，空間複雜度為 $$O(N^{2})$$。

如matrix[i][j] == 1，表示正方形可以matrix[i][j]這個點作延伸，則
> 
```dp[i][j] = min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]) + 1```

如matrix[i][j] == 0，表示正方形無法matrix[i][j]這個點作延伸，則
>```dp[i][j] = 0```

由於計算 dp[i][j] 時只需 要dp[i] 與 dp[i - 1] 行，因此可利用滾動陣列來將空間進而優化到 $$O(N)$$，狀態轉換如下：

>```dp[i % 2][j] = min(dp[(i - 1) % 2][j], dp[i % 2][j - 1], dp[(i - 1) % 2][j - 1]) + 1```


```java
public int maxSquare(int[][] matrix) {
    
    if (matrix == null || matrix.length == 0) {
        return 0;
    }
    
    int length = matrix.length;
    int width = matrix[0].length;
    int maxLength = 0;
    int[][] dp = new int[length][width];
    
    for (int i = 0; i < length; i++) {
        dp[i][0] = matrix[i][0];
        if (dp[i][0] == 1) {
            maxLength = 1;
        }
    }
    
    for (int i = 0; i < width; i++) {
        dp[0][i] = matrix[0][i];
        if (dp[0][i] == 1) {
            maxLength = 1;
        }
    }

    for (int i = 1; i < length; i++) {
        for (int j = 1; j < width; j++) {
            if (matrix[i][j] == 0) {
                dp[i][j] = 0;
            } else {
                dp[i][j] = Math.min(dp[i - 1][j], Math.min(dp[i - 1][j - 1], dp[i][j - 1])) + 1;
                maxLength = (dp[i][j] > maxLength) ? dp[i][j] : maxLength;
            }
        }
    }
    
    return maxLength * maxLength;
}
```
