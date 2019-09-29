# Balanced Binary Tree

[原題網址](http://www.lintcode.com/en/problem/balanced-binary-tree/)



\[Updated on 2019.9.29\]

可以提早檢查終止條件，若已不平衡，不需要再往下算，直接返回即可，可以節省遞迴所需的時間與空間。

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
    public boolean isBalanced(TreeNode root) {
        return maxDepth(root) != -1;
    }

    public int maxDepth(TreeNode root) {
        if( root == null ) {
            return 0;
        }

        int left = maxDepth(root.left);
        if (left == -1) {
            return -1;
        }
        int right = maxDepth(root.right);
        if (right == -1) {
            return -1;
        }

        if(Math.abs(left-right) > 1 ) {
            return -1;
        }

        return Math.max(left, right) + 1;
    }
}
```

可利用修改過後的maxdepth程式來達到我們要的目的 ，因maxdepth可幫我們算出高度，  
因此我們只要去比較高度是否差一即可，程式如下：

```java
public class Solution {
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }
        return maxDepth(root) != -1;
    }

    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);

        if (left == -1 || right == -1 || Math.abs(left - right) > 1) {
            return -1;
        }
        return Math.max(left, right) + 1;
    }
}
```

> 時間複雜度：O\(n\)

```java
public boolean isBalanced(TreeNode root) {
    return maxDepth(root) != -1;
}

public int maxDepth(TreeNode root) {
    if( root == null ) {
        return 0;
    }

    int left = maxDepth(root.left);
    int right = maxDepth(root.right);

    if( left == -1 || right == -1 || Math.abs(left-right) > 1 ) {
        return -1;
    }

    return Math.max(left, right) + 1;
}
```



