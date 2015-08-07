# Maximum Depth of Binary Tree
[原題網址](http://www.lintcode.com/en/problem/maximum-depth-of-binary-tree/)

用遞迴去作即可，程式如下
```java
public int maxDepth(TreeNode root) {
	if (root == null) {
		return 0;
	} else if (root.left == null && root.right == null) {
		return 1;
	}
		int left = maxDepth(root.left);
		int right = maxDepth(root.right);
		return Math.max(left, right) + 1;
}
```
>時間複雜度O(n)
