# Flatten Binary Tree to Linked List

[Lintcode](http://www.lintcode.com/en/problem/flatten-binary-tree-to-linked-list/)

題意：

把 Binary Tree 轉成 Linked List。

Flatten a binary tree to a fake "linked list" in pre-order traversal.

Here we use the right pointer in TreeNode as the next pointer in ListNode.

Have you met this question in a real interview? Yes
Example
```
              1
               \
     1          2
    / \          \
   2   5    =>    3
  / \   \          \
 3   4   6          4
                     \
                      5
                       \
                        6
```
Note
Don't forget to mark the left child of each node to null. Or you will get Time Limit Exceeded or Memory Limit Exceeded.

Challenge
Do it in-place without any extra memory.

解題思路：

解法一：使用stack保存右子樹，接著不斷把左子樹接到 p 的右邊，接著往右邊走，別忘了把p.left 改為 null，否則會一直循環，造成超時，但此法需要O(N)的空間。

程式碼如下：

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param root: a TreeNode, the root of the binary tree
     * @return: nothing
     */
    public void flatten(TreeNode root) {
        if (root == null) {
            return;
        }
        
        Stack<TreeNode> s = new Stack<TreeNode>();
        TreeNode p = root;
        while (p != null || !s.isEmpty()) {
            if (p.right != null) {
                s.push(p.right);  
            }
            if (p.left != null) {
                p.right = p.left;
            } else if (!s.isEmpty()){
                p.right = s.pop();
            }
            p.left = null;
            p = p.right;
        }
    }
    
}
```