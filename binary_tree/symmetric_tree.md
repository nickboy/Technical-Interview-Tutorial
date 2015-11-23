# Symmetric Tree

[Leetcode](https://leetcode.com/problems/symmetric-tree/)


題意：

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree is symmetric:
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
But the following is not:
```
    1
   / \
  2   2
   \   \
   3    3
```
Note:
Bonus points if you could solve it both recursively and iteratively.




解題思路：

遞迴法：

```java
public class Solution {
    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        return isMirror(root.left, root.right);
    }
    
    private boolean isMirror(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        } else if (p == null || q == null) {
            return false;
        }
        if (p.val != q.val) {
            return false;
        }
        
        return isMirror(p.left, q.right) && isMirror(p.right, q.left);
    }
}
```

非遞迴法：分別用que來作dfs，一棵先左再右，另一棵先右再左。

```java
public class Solution {
    public boolean isSymmetric(TreeNode root) {
        Queue<TreeNode> ql = new LinkedList<TreeNode>();
        Queue<TreeNode> qr = new LinkedList<TreeNode>();

        if(root == null) return true;
        if(root.left != null)
            ql.offer(root.left);
        if(root.right != null)
            qr.offer(root.right);

        while(ql.size() != 0 && qr.size() != 0){
            TreeNode left = ql.poll();
            TreeNode right = qr.poll();
            if(left.val != right.val 
                || (left.left == null && right.right != null)
                || (left.left != null && right.right == null)
                || (left.right == null && right.left != null)
                || (left.right != null && right.left == null))
                return false;

            if(left.left != null) ql.offer(left.left);

            if(left.right != null) ql.offer(left.right);

            if(right.right != null) qr.offer(right.right);

            if(right.left != null) qr.offer(right.left);
        }

        return ql.size() == qr.size();
    }
}
```