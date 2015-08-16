# Lowest common Ancestor

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

```java
public class Solution {
    /**
     * @param root: The root of the binary search tree.
     * @param A and B: two nodes in a Binary.
     * @return: Return the least common ancestor(LCA) of the two nodes.
     */
    private ArrayList<TreeNode> getPath2Root(TreeNode node) {
        ArrayList<TreeNode> list = new ArrayList<TreeNode>();
        while (node != null) {
            list.add(node);
            node = node.parent;
        }
        return list;
    }
    public TreeNode lowestCommonAncestor(TreeNode node1, TreeNode node2) {
        ArrayList<TreeNode> list1 = getPath2Root(node1);
        ArrayList<TreeNode> list2 = getPath2Root(node2);

        int i, j;
        for (i = list1.size() - 1, j = list2.size() - 1; i >= 0 && j >= 0; i--, j--) {
            if (list1.get(i) != list2.get(j)) {
                return list1.get(i).parent;
            }
        }
        return list1.get(i+1);
    }


}

```
