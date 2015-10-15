# Minimum Adjustment Cost

[Lintcode](http://www.lintcode.com/en/problem/minimum-adjustment-cost/)

題意：

Given an integer array, adjust each integers so that the difference of every adjacent integers are not greater than a given number target.

If the array before adjustment is A, the array after adjustment is B, you should minimize the sum of |A[i]-B[i]|

Example

Given [1,4,2,3] and target = 1, one of the solutions is [2,3,2,3], the adjustment cost is 2 and it's minimal.

Return 2.

>即給一個陣列與一個 target，試著調整每個陣列元素使得與鄰近的陣列元素大於 target值，但求最小的調整成本。

解題思路：

由於題目已規定值只有可能從1到100，我們可以根據每個的index去枚舉1到100的可能性，可使用遞迴來幫助我們，但此題複雜度太高了，為指數性的複雜度，其程式碼如下：

```java
public class Solution {
    /**
     * @param A: An integer array.
     * @param target: An integer.
     */
    public int MinAdjustmentCost(ArrayList<Integer> A, int target) {
        if (A == null) {
            return 0;
        }
        
        return helper(A, new ArrayList<Integer>(A), target, 0);
    }
    
    public int helper(ArrayList<Integer> A, ArrayList<Integer> B, int target, int index) {
        int len = A.size();
        if (index >= len) {
            return 0;
        }
        
        int diff = 0;
        
        int min = Integer.MAX_VALUE;
        for (int i = 0; i <= 100; i++) {
            if (index != 0 && Math.abs(i - B.get(index - 1)) > target) {
                continue;
            }
            B.set(index, i);
            diff = Math.abs(i - A.get(index));
            diff += helper(A, B, target, index + 1);
            min = Math.min(min, diff);
            
            B.set(index, A.get(index));
        }
        
        return min;
    }
}
```

不過我們可以透過memory search來避免重複的運算，其程式碼如下：

>M[i][j] 表示該該陣列第i個元素為j的最小成本為多少。

>M[i][j]的定義是：從index = i處開始往後所有的differ，並且A[i]的取值取為j + 1;

```
public class Solution {
    /**
     * @param A: An integer array.
     * @param target: An integer.
     */
    int[][] M;
    public int MinAdjustmentCost(ArrayList<Integer> A, int target) {
        if (A == null) {
            return 0;
        }
        M = new int[A.size()][100];
        for (int i = 0; i < A.size(); i++) {
            for (int j = 0; j < 100; j++) {
                M[i][j] = Integer.MAX_VALUE;
            }
        }
        return helper(A, new ArrayList<Integer>(A), target, 0);
    }
    
    public int helper(ArrayList<Integer> A, ArrayList<Integer> B, int target, int index) {
        int len = A.size();
        if (index >= len) {
            return 0;
        }
        
        int diff = 0;
        
        int min = Integer.MAX_VALUE;
        for (int i = 1; i <= 100; i++) {
            if (index != 0 && Math.abs(i - B.get(index - 1)) > target) {
                continue;
            }
            
            // 只要之前計算過了，直接返回
            if (M[index][i - 1] != Integer.MAX_VALUE) {
                diff = M[index][i - 1];
                min = Math.min(min, diff);
                continue;
            }
            B.set(index, i);
            diff = Math.abs(i - A.get(index));
            
            diff += helper(A, B, target, index + 1);
            min = Math.min(min, diff);
            M[index][i - 1] = diff; //紀錄在該index而值為i的最小成本為多少
            
            B.set(index, A.get(index));
        }
        
        return min;
    }
}
```

