#Subtree

[]()

題意：給定兩棵樹 T1 與 T2 ，檢查 T2 是否為 T1 的子樹。


解題思路：使用 Divide and Conquer 來解這道題，其程式碼如下：

```java

public class Solution {
    /**
     * @param T1, T2: The roots of binary tree.
     * @return: True if T2 is a subtree of T1, or false.
     */
    public boolean isSubtree(TreeNode t1, TreeNode t2) {
        boolean res = false;
        
        if (t1 != null && t2 != null) {
            if (t1.val == t2.val) {
                res = doesTree1HaveTree2(t1, t2);
            }
            
            if (!res) {
                res = isSubtree(t1.left, t2);
            }
            
            if (!res) {
                res = isSubtree(t1.right, t2);
            }
        }
        
        return res;
    }
    
    private boolean doesTree1HaveTree2(TreeNode t1, TreeNode t2) {
        if (t2 == null) {
            return true;
        }
        
        if (t1 == null) {
            return false;
        }
        
        if (t1.val != t2.val) {
            return false;
        }
        
        return doesTree1HaveTree2(t1.left, t2.left) && doesTree1HaveTree2(t1.right, t2.right);
        
    }
}

```

---
###Reference
1. 劍指 Offer 第三章