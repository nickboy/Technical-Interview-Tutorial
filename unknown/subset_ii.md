# Subset II

[Leetcode](https://leetcode.com/problems/subsets-ii/)

題意：

Given a collection of integers that might contain duplicates, nums, return all possible subsets.

Note:
Elements in a subset must be in non-descending order.
The solution set must not contain duplicate subsets.
For example,
If nums = [1,2,2], a solution is:
```
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

解題思路：

如果有重複的話，不能跳著取。

```java
public class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();

        if (nums == null || nums.length == 0) {
            return res;   
        }

        Arrays.sort(nums);

        helper(nums, 0, new ArrayList<Integer>(), res);
        return res;
    }

    private void helper(int[] nums, int pos, List<Integer> tempRes, List<List<Integer>> res) {
        if (pos > nums.length) {
            return;
        }

        res.add(new ArrayList<Integer>(tempRes));
        for (int i = pos; i < nums.length; i++) {
            if (i == pos || nums[i - 1] != nums[i]) {
                tempRes.add(nums[i]);
                helper(nums, i + 1, tempRes, res);
                tempRes.remove(tempRes.size() - 1);
            }
        }
    }
}
```