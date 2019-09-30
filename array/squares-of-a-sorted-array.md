# Squares of a Sorted Array

##### 題目連結：

[https://leetcode.com/problems/squares-of-a-sorted-array/](https://leetcode.com/problems/squares-of-a-sorted-array/)

##### 題意：

給定一個有序陣列，將每個元素取平方後再排序。

**Example 1:**

```
Input: 
[-4,-1,0,3,10]
Output: 
[0,1,9,16,100]
```

**Example 2:**

```
Input: 
[-7,-3,2,3,11]
Output: 
[4,9,9,49,121]
```

##### 解法：

由於是有序陣列，且取平方後無論是正數或是負數，絕對值大的數想乘為最大，因此我們可以使用兩根指針的方式，不斷的比較兩數的絕對值，並且倒著寫入新的陣列。

```java
class Solution {
    public int[] sortedSquares(int[] A) {
        if (A == null || A.length == 0) {
            return A;
        }
        
        int length = A.length;
        int[] result = new int[length];
        int cur = length - 1;
        int left = 0;
        int right = length - 1;
        
        while (left <= right) {
            if (Math.abs(A[left]) > Math.abs(A[right])) {
                result[cur] = A[left] * A[left];
                left++;
            } else {
                result[cur] = A[right] * A[right];
                right--;
            }
            cur--;
        }
        
        return result;
    }
}
```

##### Complexity:

* Time: $$O(N)$$ ，因只使遍歷一次陣列。
* Space: $$O(N)$$，因需要一陣列來存下答案。

##### Reference:

* [https://leetcode.com/problems/squares-of-a-sorted-array/solution/](https://leetcode.com/problems/squares-of-a-sorted-array/solution/)



