# Combination Sum III

[Leetcode](https://leetcode.com/problems/combination-sum-iii/)


題意：

Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

Ensure that numbers within the set are sorted in ascending order.


Example 1:

Input: k = 3, n = 7

Output:
```
[[1,2,4]]
```
Example 2:

Input: k = 3, n = 9

Output:
```
[[1,2,6], [1,3,5], [2,3,4]]
```
解題思路：

為 combination sum的變形，給一個數字k與n，k表示組合中的元素個數，n表示目標值，元素只有從1-9。

需要特別注意的就是是否滿足條件，若超出元素個數或是往下加已超過目標值的話，直接prune。

```java
public class Solution {
    List<List<Integer>> res;
    public List<List<Integer>> combinationSum3(int k, int n) {
        res = new ArrayList<List<Integer>>();
        if (k == 0 || n == 0) {
            return res;
        }
        helper(k, n, 0, 1, new ArrayList<Integer>());
        return res;
    }
    
    private void helper(int k, int n, int sum, int pos, List<Integer> tempRes) {
        if (tempRes.size() == k) {
            if (n == sum) {
                res.add(new ArrayList<Integer>(tempRes));
            }
            return;
        }
        
        for (int i = pos; i <= 9; i++) {
            if ((sum + i) > n || tempRes.size() == k) {
                break;
            } else {
                tempRes.add(i);
                helper(k, n, sum + i, i + 1, tempRes);
                tempRes.remove(tempRes.size() - 1);
            }
        }
    }
}
```