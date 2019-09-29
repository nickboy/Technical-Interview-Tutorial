# Second Minimum Node In a Binary Tree

##### 原題網址：

##### [https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/](https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/)

##### 題意：

給定一個Binary Tree，找出第二小的node，假設所有node的值都一樣代表無第二小的node，返回-1。

**Example 1:**

```
Input:
 
    2
   / \
  2   5
     / \
    5   7


Output:
 5

Explanation:
 The smallest value is 2, the second smallest value is 5.
```

**Example 2:**

```
Input:
 
    2
   / \
  2   2


Output:
 -1

Explanation:
 The smallest value is 2, but there isn't any second smallest value.
```

##### 解題思路：

由於非BST，所以仍需走訪所有節點才知道結果，我們可以使用DFS，與維護兩個數值**First**與**Second**，最後則返回**Second**即可。



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
    public int findSecondMinimumValue(TreeNode root) {
        
        if (root == null) {
            return -1;
        }
        
        int first = root.val;
        long second = Integer.MAX_VALUE;
        
        Stack<TreeNode> stack = new Stack<>();
        TreeNode current = root;
        
        while (!stack.isEmpty() || current != null) {
            while (current != null) {
                stack.push(current);
                current = current.left;
            }
            
            current = stack.pop();
            if (current.val > first && current.val < second) {
                second = current.val;
            } else if (current.val < first) {
                first = current.val;
            }
            
            current = current.right;
        }
        
        return (second == Integer.MAX_VALUE) ? -1 : second;
        
    }
```

##### Complexity:

時間：O\(N\)，因需走訪所有節點。

空間：O\(1\)，只需維護First與Second值即可。

##### Reference:

* [https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/solution/](https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/solution/)

* [https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/discuss/107158/Java-divide-and-conquer-solution](https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/discuss/107158/Java-divide-and-conquer-solution)



