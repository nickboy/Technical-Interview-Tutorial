# Subsets

[Leetcode](https://leetcode.com/problems/subsets/)

**題意：**

Given a set of distinct integers, nums, return all possible subsets.

Note:
Elements in a subset must be in non-descending order.
The solution set must not contain duplicate subsets.
For example,
If nums = [1,2,3], a solution is:
```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

**解題思路：**

**Backtracking:**
```java
public class Solution {
    public List<List<Integer>> subsets(int[] nums) {
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
            tempRes.add(nums[i]);
            helper(nums, i + 1, tempRes, res);
            tempRes.remove(tempRes.size() - 1);
        }
    }
}
```

非遞迴：

```java
public class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        res.add(new ArrayList<Integer>());
        if (nums == null || nums.length == 0) {
            return res;   
        }
        
        Arrays.sort(nums);
        
        for (int i = 0; i < nums.length; i++) {
            int size = res.size();
            for (int j = 0; j < size; j++) {
                List<Integer> tempRes = new ArrayList<Integer>(res.get(j));
                tempRes.add(nums[i]);
                res.add(tempRes);
            }
        }
        
        return res;
    }
    
    
}
```

Bit manipulation:

```java
public class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();

        if (nums == null || nums.length == 0) {
            return res;   
        }
        
        Arrays.sort(nums);
        
        int powerOfTwo = (int)Math.pow(2, nums.length);
        for (int i = 0; i < powerOfTwo; i++) {
            List<Integer> list = new ArrayList<>();
            for (int j = 0; j < nums.length; j++) {
                if (((i >> j) & 1) == 1) {
                    list.add(nums[j]);
                }
            }
            res.add(list);
        }
        
        return res;
    }
    
    
}
```