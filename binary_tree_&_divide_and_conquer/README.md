#Binary Tree & Divide and Conquer

**Template**
1. Traversal(DFS)
Build a traverse function and call it in main function
```java
// preorder example
public void traverse( resultType result, TreeNode node) {
    if ( node == null ) {     -> condition for leaves
        return;
    }
    result.add(node.val);    -> add the value
    traverse(result, node.left);
    traverse(result, node.right);
}
```

2. Divide and Conquer (DFS)
分別去跑，最後再把結果合起來

```java
public class Solution {
    public ArrayList<Integer> preorderTraversal(TreeNode root) {
        ArrayList<Integer> result = new ArrayList<Integer>();
        // null or leaf
        if (root == null) {
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
}
```

-----

**Maximum Depth of Binary Tree**
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

---
**Balanced Binary Tree**
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
 >時間複雜度：O(n)

---
**Lowestommon Ancestor**

當每個節點只有left與right兩個指針時，使用以下解法，
如果A和B都在root裡，返回A和B的最近公共祖先
如果只有a在root為根的子樹裡，返回a
如果只有b在root為根的子樹裡，返回b
如果都不在，返回null
```java
public class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode A, TreeNode B) {
        // write your code here
        if (root == null) {
            return null;
        }

        //因題目說a或b可包含在root內，因此判斷若a或b為root，則直接返回root
        if (root == A || root == B) {
            return root;
        }
        TreeNode left = lowestCommonAncestor(root.left, A, B);
        TreeNode right = lowestCommonAncestor(root.right, A, B);

        //代表左右子樹都找不到以ab為代表的最低共同父節點，因此返回根節點
        if (left != null && right != null) {
            return root;
        }
        //返回其中之一不為空的結果即可
        return left != null? left:right;
    }
}
```

若是只有父節點的話，先把兩個節點到root的path列出來，接著一一比較，一直比較到不同的上一個則是最低共同父節點


