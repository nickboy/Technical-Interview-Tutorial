# N-Queen II

[Leetcode](https://leetcode.com/problems/n-queens-ii/)

題意：

Follow up for N-Queens problem.

Now, instead outputting board configurations, return the total number of distinct solutions.

解題思路：

比 [N-Queen I]() 還簡單，只需要算出總共有多少解法即可，把draw function改成coun++即可。

程式碼如下：


```java
public class Solution {
    int count = 0;
    public int totalNQueens(int n) {
        if (n == 0) {
            return count;
        }
        
        helper(new ArrayList<Integer>(), n);
        return count;
    }
    
    private void helper(List<Integer> tempRes, int n) {
        if (tempRes.size() == n) {
            count++;
            return;
        }
        
        for (int i = 0; i < n; i++) {
            if (isValid(tempRes, i)) {
                tempRes.add(i);
                helper(tempRes, n);
                tempRes.remove(tempRes.size() - 1);
            }
        }
    }
    
    private boolean isValid(List<Integer> tempRes, int pos) {
        int len = tempRes.size();
        for (int i = 0; i < len; i++) {
            if (tempRes.get(i) == pos) {
                return false;
            }
            
            if (len + pos == i + tempRes.get(i)) {
                return false;
            }
            
            if (len - pos == i - tempRes.get(i)) {
                return false;
            }
        }
        
        return true;
    }
}
```