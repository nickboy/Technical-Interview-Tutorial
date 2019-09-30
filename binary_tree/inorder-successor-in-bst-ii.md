# Inorder Successor in BST II

##### 題目連結：

* [https://leetcode.com/problems/inorder-successor-in-bst-ii/](https://leetcode.com/problems/inorder-successor-in-bst-ii/)
* 此題亦出現在CTCI第6版中第4章中。

##### 題意：

給定一個BST與一個Node x，找出該節點的中序後繼者。

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/01/23/285_example_1.PNG)

```
Input: 

root = 
{"$id":"1","left":{"$id":"2","left":null,"parent":{"$ref":"1"},"right":null,"val":1},"parent":null,"right":{"$id":"3","left":null,"parent":{"$ref":"1"},"right":null,"val":3},"val":2}

p = 
1
Output: 
2
Explanation: 
1's in-order successor node is 2. Note that both p and the return value is of Node type.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/01/23/285_example_2.PNG)

```
Input: 

root = 
{"$id":"1","left":{"$id":"2","left":{"$id":"3","left":{"$id":"4","left":null,"parent":{"$ref":"3"},"right":null,"val":1},"parent":{"$ref":"2"},"right":null,"val":2},"parent":{"$ref":"1"},"right":{"$id":"5","left":null,"parent":{"$ref":"2"},"right":null,"val":4},"val":3},"parent":null,"right":{"$id":"6","left":null,"parent":{"$ref":"1"},"right":null,"val":6},"val":5}

p = 
6
Output: 
null
Explanation: 
There is no in-order successor of the current node, so the answer is 
null
.
```

##### 解法：

* 若有右子樹，則直接拿右子樹最左邊那個節點即可。
* 若無右子樹，表示此節點可能為當下子樹中最後一個被訪問的節點，所以我們必須找出一個節點，且當下node x所在的子樹為該節點的左子樹。如果找不到，則反回null。

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node parent;
};
*/
class Solution {
    public Node inorderSuccessor(Node x) {
        if (x == null) {
            return x;
        }
        
        if (x.right != null) {
            // 若有右子樹，則直接拿右子樹最左邊那個節點即可。
            Node succ = x.right;
            while (succ.left != null) {
                succ = succ.left;
            }
            return succ;
        } else {
            // 若無右子樹，表示此節點可能為當下子樹中最後一個被訪問的節點，
            // 所以我們必須找出一個節點，且當下node x所在的子樹為該節點的左子樹。
            // 如果找不到，則反回null。
            Node current = x;
            Node parent = current.parent;
            while (parent != null && parent.left != current) {
                current = parent;
                parent = parent.parent;
            }
            return parent;
        }
    }
}
```

##### Reference:

* [https://leetcode.com/problems/inorder-successor-in-bst-ii/solution/](https://leetcode.com/problems/inorder-successor-in-bst-ii/solution/)



