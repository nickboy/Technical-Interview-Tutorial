# Count Complete Tree Nodes

[]()

題意：

Given a complete binary tree, count the number of nodes.


解題思路：

網友 [書影](http://bookshadow.com/weblog/2015/06/06/leetcode-count-complete-tree-nodes/) 提供了以下思路：

遞迴法：分別列舉左右子樹的高度，如果兩者一樣，表示此子樹為full bt，因此直接返回 $$2^h - 1$$即可，否則繼續往下遞迴，此法複雜度為指數型，leetcode無法通過。

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
    public int countNodes(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        TreeNode leftNode = root;
        TreeNode rightNode = root;
        int leftHeight = 0;
        int rightHeight = 0;
        while(leftNode != null) {
            leftNode = leftNode.left;
            leftHeight++;
        }
        while(rightNode != null) {
            rightNode = rightNode.right;
            rightHeight++;
        }
        
        if (rightHeight == leftHeight) {
            return (int)Math.pow(2, rightHeight) - 1; // 因pow會回傳double
        } else {
            return countNodes(root.left) + countNodes(root.right) + 1; //加上root本身的那個節點，因此加一
        }
    }
}
```



---
###Reference
1. http://bookshadow.com/weblog/2015/06/06/leetcode-count-complete-tree-nodes/