# Range Sum Query - Mutable

[Leetcode](https://leetcode.com/problems/range-sum-query-mutable/)

**題意：**

Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

The update(i, val) function modifies nums by updating the element at index i to val.
Example:
Given nums = [1, 3, 5]
```
sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```
**Note:**
The array is only modifiable by the update function.
You may assume the number of calls to update and sumRange function is distributed evenly.



**解題思路：**

一樣是使用線段樹來幫忙解決這問題，因為他會不斷的修改，線段樹可達到O(logN)的RMQ複雜度。

```java
public class NumArray {
    SegmentTree segmentTree;
    public NumArray(int[] nums) {
        segmentTree = new SegmentTree(nums);
        
    }

    void update(int i, int val) {
        segmentTree.update(i, val);
    }

    public int sumRange(int i, int j) {
        return segmentTree.sumRange(i, j);
    }
}

class SegmentTreeNode {
    int start;
    int end;
    int sum;
    SegmentTreeNode left;
    SegmentTreeNode right;
    public SegmentTreeNode(int start, int end) {
        this.start = start;
        this.end = end;
        this.sum = 0;
        left = null;
        right = null;
    }
}

class SegmentTree {
    SegmentTreeNode root;
    
    public SegmentTree(int[] nums) {
        root = buildST(nums, 0, nums.length - 1);
    }
    
    public SegmentTreeNode buildST(int[] nums, int start, int end) {
        if (start > end) {
            return null;
        }
        
        SegmentTreeNode root = new SegmentTreeNode(start, end);
        if (start == end) {
            root.sum = nums[start];
            return root;
        }
        
        int mid = start + (end - start) / 2;
        root.left = buildST(nums, start, mid);
        root.right = buildST(nums, mid + 1, end);
        
        root.sum = root.left.sum + root.right.sum;
        
        return root;
    }
    
    public void update (int pos, int val) {
        update(root, pos, val);
    }
    
    public void update(SegmentTreeNode root, int pos, int val) {
        if (root.start == root.end) {
            root.sum = val;
            return;
        }
        
        int mid = root.start + (root.end - root.start) / 2;
        if (pos <= mid) {
            update(root.left, pos, val);
        } else {
            update(root.right, pos, val);
        }
        
        root.sum = root.left.sum + root.right.sum;
    }
    
    public int sumRange(int start, int end) {
        return sumRange(root, start, end);
    }
    
    public int sumRange(SegmentTreeNode root, int start, int end) {
        if (root.start == start && root.end == end) {
            return root.sum;
        }
        
        int mid = root.start + (root.end - root.start) / 2;
        if (start >= mid + 1) {
            return sumRange(root.right, start, end);
        } else if (end <= mid) {
            return sumRange(root.left, start, end);
        }
        
        return sumRange(root.left, start, mid) + sumRange(root.right, mid + 1, end);
    }
}





// Your NumArray object will be instantiated and called as such:
// NumArray numArray = new NumArray(nums);
// numArray.sumRange(0, 1);
// numArray.update(1, 10);
// numArray.sumRange(1, 2);
```