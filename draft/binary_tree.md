# Binary Tree

樹在現實的系統裡是常見的資料結構，


* 前序 Pre-order

[原題網址](http://www.lintcode.com/en/problem/binary-tree-preorder-traversal/)

```java
public ArrayList<Integer> preorderTraversal(TreeNode root) {
    // write your code here
    ArrayList<Integer> result = new ArrayList<Integer>();
    
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
```

```java
public ArrayList<Integer> preorderTraversal(TreeNode root) {
    // write your code here
    ArrayList<Integer> result = new ArrayList<Integer>();
    traverse(result, root);
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
非遞迴

```java
public ArrayList<Integer> preorderTraversal(TreeNode root) {
    ArrayList<Integer> result = new ArrayList<Integer>();
    if ( root == null ) {
        return result;
    }
    
    Stack<TreeNode> stack = new Stack<TreeNode>();
    stack.push(root);
    
    while ( !stack.isEmpty() ) {
        TreeNode current = stack.pop();
        result.add(current.val);
        if ( current.right != null ) {
            stack.push(current.right);
        }
        if ( current.left != null ) {
            stack.push(current.left);
        }
    }
    return result;
}
```

* 中序 In-order

[原題網址](http://www.lintcode.com/en/problem/binary-tree-inorder-traversal/)

```java
public ArrayList<Integer> inorderTraversal(TreeNode root) {
    ArrayList<Integer> result = new ArrayList<Integer>();
    
    traverse(result, root);
    return result;
}

public void traverse(ArrayList<Integer> result, TreeNode node) {
    if ( node == null ) {
        return;
    }
    
    traverse(result, node.left);
    result.add(node.val);
    traverse(result, node.right);
}
```

```java
public ArrayList<Integer> inorderTraversal(TreeNode root) {
    ArrayList<Integer> result = new ArrayList<Integer>();
    if ( root == null ) {
        return result;
    }

    ArrayList<Integer> left = inorderTraversal(root.left);
    ArrayList<Integer> right = inorderTraversal(root.right);
    
    result.addAll(left);
    result.add(root.val);
    result.addAll(right);
    
    return result;
}
```

非遞歸
```java
public ArrayList<Integer> inorderTraversal(TreeNode root) {
    ArrayList<Integer> result = new ArrayList<Integer>();
    if ( root == null ) {
        return result;
    }
    
    Stack<TreeNode> stack = new Stack<TreeNode>();
    
    TreeNode current = root;
    while ( current != null || !stack.isEmpty() ) {
        while ( current != null ) {
            stack.push(current);
            current = current.left;
        }
        current = stack.pop();
        result.add(current.val);
        current = current.right;
    }
    return result;
}
```
* 後序 Post-order

[原題網址](http://www.lintcode.com/en/problem/binary-tree-postorder-traversal/)


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
