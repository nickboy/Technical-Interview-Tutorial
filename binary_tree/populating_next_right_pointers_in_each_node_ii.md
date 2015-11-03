# Populating Next Right Pointers in Each Node ii

[Leetcode](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)

題意：

與第一題相同，只是不同的是這次的二元樹是任意的，不再是complete bt了。

解題思路：


```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        if (root == null) {
            return;
        }
        
        
        // p為上一層像linked list走訪的節點
        // first為下一層的第一個節點，last用來走訪下一層的linked list
        TreeLinkNode p = root;
        TreeLinkNode first = null;
        TreeLinkNode last = null;
        
        while (p != null) {
            if (first == null) {
                if (p.left != null) {
                    first = p.left;
                } else if (p.right != null) {
                    first = p.right;
                }
            }
            
            
            if (p.left != null) {
                if (last != null) {
                    last.next = p.left;
                }
                last = p.left;
            }
            
            if (p.right != null) {
                if (last != null) {
                    last.next = p.right;
                }
                last = p.right;
            }
            
            if (p.next != null) {
                // 移到下一個的sibling
                p = p.next;
            } else { 
                // 換到下一層
                p = first;
                first = null;
                last = null;
            }
        }
    }
}
```

----
###Reference
1. https://siddontang.gitbooks.io/leetcode-solution/content/tree/populating_next_right_pointers_in_each_node.html