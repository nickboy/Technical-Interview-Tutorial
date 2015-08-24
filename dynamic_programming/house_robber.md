#House Robber

[]()

題意：給予一陣列，陣列中每一元素代表每個家的財產，小偷不能連續偷兩間房，求最大獲利。

解題思路：使用動態規劃來作，程式碼如下：

```java
public long houseRobber(int[] A) {
    
    if (A == null || A.length <= 3) {
        if (A == null || A.length == 0) {
            return 0;
        } else if (A.length == 1) {
            return A[0];
        } else if (A.length == 2) {
            return Math.max(A[0], A[1]);
        } else if (A.length == 3) {
            return  Math.max((A[0] + A[2]), A[1]);
        }
    }
    
    int len = A.length;
    long[] profit = new long[len];
    profit[0] = A[0];
    profit[1] = Math.max(A[0], A[1]);
    profit[2] = Math.max((A[0] + A[2]), A[1]);
    
    for (int i = 3; i < len; i++) {
        profit[i] = Math.max(profit[i-1], profit[i-2] + A[i]);
    }
    
    return profit[len-1];
}
```

>Time Complexity：$$O(N)$$，只需遍歷一次陣列即可。

>Space Complexity： $$O(N)$$，此可用滾動陣列來優化到 $$O(1)$$。