# Remove Node in Binary Search Tree

[原題網址](http://www.lintcode.com/en/problem/remove-node-in-binary-search-tree/)

> Given a root of Binary Search Tree with unique value for each node.  Remove the node with given value. If there is no such a node with given value in the binary search tree, do nothing. You should keep the tree still a binary search tree after removal.

> 刪除二元搜索樹中的一個節點

先找到要刪除的節點，若不是現在的節點，根據大小往左或往右繼續找下去。若找到就呼叫刪除的函數 `removeRoot(TreeNode root, int value)` 。
```java
public TreeNode removeNode(TreeNode root, int value) {
    // write your code here
    if ( root == null ) {
        return null;
    }
    
    if ( root.val == value ) {      // romove from root;
        root = removeRoot(root, value);
    } else if ( value > root.val ) {
        root.right = removeNode(root.right, value);
    } else {
        root.left = removeNode(root.left, value);
    }
    return root;
}
```


```java
public TreeNode removeRoot(TreeNode root, int value) {
    
    if ( root.left == null && root.right == null ) {
        return null;
    } else 
    if ( root.left == null || root.right == null ) {
        if ( root.left == null ) {
            return root.right;
        } else {
            return root.left;
        }
    } else {
        if ( root.left.right == null ) {
            root.left.right = root.right;
            return root.left;
        } else if ( root.right.left == null ) {
            root.right.left = root.left;
            return root.right;
        } else {
            TreeNode target = findMax(root.left);
            target.left = removeNode(root.left, target.val);
            target.right = root.right;
            return target;
        }
    }
}

public TreeNode findMax(TreeNode root) {
    while ( root != null && root.right != null ) {
        root = root.right;
    }
    return root;
}
```