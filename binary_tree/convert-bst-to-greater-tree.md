# Convert BST to Greater Tree

###### 題意：

Given a Binary Search Tree \(BST\), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus sum of all keys greater than the original key in BST.

######  Example:

```
 The root of a Binary Search Tree like this:
              5
            /   \
           2     13


Output:
 The root of a Greater Tree like this:
             18
            /   \
          20     13
```

###### 解法：

由於只有比該node的值大的node，才會影響到該node的值，因此我們可以利用**Reverse Inorder Traversal**來遍歷一整棵樹，並維護一個**Sum**值，該Sum值即是紀錄著當下node之前所有比該node大的所有node的值之和。

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
class Solution {
    
    int sum = 0;
    public TreeNode convertBST(TreeNode root) {
        convert(root);
        return root;
    }
    
    public void convert(TreeNode root) {
        if (root == null) {
            return;
        }
        
        convert(root.right);
        root.val = sum + root.val;
        sum = root.val;
        convert(root.left);
    }
}
```

###### Complexity:

Time: O\(N\)，N為node數量

Space: O\(1\)，因為我們只需一個sum值並且我們是直接修改原本的BST。

###### Reference: 

* [https://leetcode.com/problems/convert-bst-to-greater-tree/discuss/100506/Java-Recursive-O\(n\)-time](https://leetcode.com/problems/convert-bst-to-greater-tree/discuss/100506/Java-Recursive-O%28n%29-time)



