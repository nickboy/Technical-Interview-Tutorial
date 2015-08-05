# Insert Node in a Binary Search Tree

```java
public class Solution {
    /**
     * @param root: The root of the binary search tree.
     * @param node: insert this node into the binary search tree
     * @return: The root of the new binary search tree.
     */
    public TreeNode insertNode(TreeNode root, TreeNode node) {
        // write your code here
        if (root == null) {
            return node;
        }
        TreeNode cur = root;
        TreeNode prev = null;
        while (cur != null) {
            prev = cur;
            if (cur.val < node.val) {
                cur = cur.right;
            } else if (cur.val > node.val) {
                cur = cur.left;
            }
        }
        if (prev.val < node.val) {
            prev.right = node;
        } else {
            prev.left = node;
        }
        return root;
    }
}
```
