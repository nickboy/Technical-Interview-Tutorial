# Previous Permutation

[Lintcode](http://www.lintcode.com/en/problem/previous-permutation/)


題意：

給定一個組合，找出前一組

解題思路：

其是是next permutation的 reverse，只要把以下條件改過來即可

演算法如下：
>由右往左找出第一個位置i使得i+1位數的數比它小，如果最後i為-1，表示排列為升序，為第一個排列，所以前一個就是反序直接把序列整個reverse即可。

>再由最後一位到pivot中間找一個元素j，使得nums[j] < nums[pivot]，並將兩者交換

> 交換後，把pivot後面那一段整個reverse即可

程式碼如下：

```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: A list of integers that's previous permuation
     */
    public ArrayList<Integer> previousPermuation(ArrayList<Integer> nums) {
		if (nums == null || nums.size() < 2) {
            return nums;
        }
        
        int len = nums.size();
        int pivot = -1;
        
        for (int i = len - 2; i >= 0; i--) {
            if (nums.get(i) > nums.get(i+1)) {
                pivot = i;
                break;
            }
        }
        
        if (pivot != -1) {
            for (int i = len - 1; i > pivot; i--) {
                if (nums.get(i) < nums.get(pivot)) {
                    swap(nums, i, pivot);
                    break;
                }
            }
        }
        
        reverse(nums, pivot + 1, len - 1);
        
        return nums;
    }
    
    private ArrayList<Integer> reverse(ArrayList<Integer> list, int start, int end) {
        while (start < end) {
            int temp = list.get(start);
            list.set(start, list.get(end));
            list.set(end, temp);
            start++;
            end--;
        }
        return list;
    }
    
    private void swap(ArrayList<Integer> list, int i, int j) {
        int temp = list.get(i);
        list.set(i, list.get(j));
        list.set(j, temp);
    }
}
```
---
###Reference
1. http://www.cnblogs.com/tonix/p/4916200.html
2. 