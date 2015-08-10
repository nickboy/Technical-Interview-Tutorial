# Binary Tree Level Order Traversal

[原題網址](http://www.lintcode.com/en/problem/binary-tree-level-order-traversal/)

```java
public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
    ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
    if ( root == null ) {
        return result;
    }
    
    Queue<TreeNode> queue = new LinkedList<TreeNode>();
    queue.offer(root);
    
    while ( !queue.isEmpty() ) {
        ArrayList<Integer> level = new ArrayList<Integer>();
        int size = queue.size();
        for ( int i = 0 ; i < size ; i++ ) {
            TreeNode current = queue.poll();
            if ( current.left != null ) {
                queue.offer(current.left);
            }
            if ( current.right != null ) {
                queue.offer(current.right);
            }
            level.add(current.val);
        }
        result.add(level);
    }
    return result;
}
```

