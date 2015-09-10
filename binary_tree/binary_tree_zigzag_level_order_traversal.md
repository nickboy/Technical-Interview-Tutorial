#Binary Tree Zigzag Level Order Traversal

[原題網址](http://www.lintcode.com/en/problem/binary-tree-zigzag-level-order-traversal/)

題意：

Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).


解題思路：使用level order traversal，再加上queue與stack的幫助。

程式碼如下，但有錯誤，待發現bug再回頭修正

```java
public ArrayList<ArrayList<Integer>> zigzagLevelOrder(TreeNode root) {
    
    ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>>();
    if (root == null) {
        return null;
    }
    
    int level = 1;
    Stack<TreeNode> stack = new Stack<TreeNode>();
    Queue<TreeNode> queue = new LinkedList<TreeNode>();
    Queue<TreeNode> traverseQ = new LinkedList<TreeNode>();
    
    traverseQ.offer(root);
    while (!traverseQ.isEmpty()) {
        int size = traverseQ.size();
        
        for (int i = 0; i < size; i++) {
            TreeNode cur = traverseQ.poll();
            if (level % 2 == 1) {
                queue.offer(cur);
            } else {
                stack.push(cur);
            }
            
            if (cur.left != null) {
                traverseQ.offer(cur.left);
            }
            
            if (cur.right != null) {
                traverseQ.offer(cur.right);
            }
        }
        
        List<Integer> tempRes = new ArrayList<Integer>();
        if (level % 2 == 1) {
            for (int i = 0; i < queue.size(); i++) {
                tempRes.add(queue.poll().val);
            }
        } else {
            for (int i = 0; i < stack.size(); i++) {
                tempRes.add(stack.pop().val);
            }
        }
        
        res.add(new ArrayList<Integer>(tempRes));
        level++;
    }
    
    return res;
}
```