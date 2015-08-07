# Binary Tree

樹在現實的系統裡是常見的資料結構，


* 前序 Pre-order

```java
public ArrayList<Integer> preorderTraversal(TreeNode root) {
    // write your code here
    ArrayList<Integer> result = new ArrayList<Integer>();
    // traverse(result, root);
    
    if ( root == null ) {
        return result;
    }
    
    // Divide
    ArrayList<Integer> left = preorderTraversal(root.left);
    ArrayList<Integer> right = preorderTraversal(root.right);
    
    // Conquer
    result.add(root.val);
    result.addAll(left);
    result.addAll(right);
    
    return result;
}

public void traverse(ArrayList<Integer> result, TreeNode node) {
    if ( node == null ) {
        return;
    }
    result.add(node.val);
    traverse(result, node.left);
    traverse(result, node.right);
}
```

* 中序 In-order

* 後序 Post-order




方法：
D&C
Traversal
non-recursion

Binary Search Tree
The left subtree of a node contains only nodes with keys **less than** the node's key.
The right subtree of a node contains only nodes with keys **greater than** the node's key.
Both the left and right subtrees must also be binary search trees.
Inorder of BST is a sorted order.
Don’t mess up with Heap  (http://cs.stackexchange.com/questions/27860/whats-the-difference-between-a-binary-search-tree-and-a-binary-heap)
