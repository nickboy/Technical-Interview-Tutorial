#Kth Smallest Element in a BST

[原題網址](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

題意：找出 BST 中第 k 大的元素。


解題思路：

暴力法花 O(K)，利用中序遍歷樹中每個節點後存到一個 list， 接著把list中第k個元素抓出來即可。

```java
public class Solution {
    public int kthSmallest(TreeNode root, int k) {
        
        if (root == null) {
            return 0;
        }
        
        List<Integer> res = new ArrayList<Integer>();
        helper(res, root);
        
        if (k > res.size()) {
            return 0;
        } else {
            return res.get(k - 1);
        }
        
    }
    
    private void helper(List<Integer> list, TreeNode root) {
        if (root == null) {
            return;
        }
        
        helper(list, root.left);
        list.add(root.val);
        helper(list, root.right);
    }
}
```