# Closest Binary Search Tree Value

[Leetcode](https://leetcode.com/problems/closest-binary-search-tree-value/)

題意：

給一個target，找一個最接近target的節點


Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

Note:

Given target value is a floating point.
You are guaranteed to have only one unique value in the BST that is closest to the target.



解題思路：

法一：遞迴

不斷的拿diff去比較，回傳差距最小的那個節點的值

程式碼如下：

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public int closestValue(TreeNode root, double target) {
        if (root == null) {
            return Integer.MAX_VALUE;
        } 
        if (root.left == null && root.right == null) {
            return root.val;
        }
        
        int left = closestValue(root.left, target);
        int right = closestValue(root.right, target);
        double rootDiff = Math.abs(root.val - target);
        double leftDiff = Math.abs(target - left);
        double rightDiff = Math.abs(target - right);
        
        if (rootDiff < leftDiff) {
            return (rootDiff < rightDiff) ? root.val : right;
        } else {
            return (leftDiff < rightDiff) ? left : right;
        }
    }
}
```