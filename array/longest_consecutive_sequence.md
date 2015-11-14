# Longest Consecutive Sequence

[Leetcode](https://leetcode.com/problems/longest-consecutive-sequence/)

題意：

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example,

Given [100, 4, 200, 1, 3, 2],

The longest consecutive elements sequence is [1, 2, 3, 4]. Return its length: 4.

Your algorithm should run in O(n) complexity.

解題思路：

通常不排序又需要O(n)的解法會需要用到hashmap或是hashset，此題就是個例子，我們先將所有數加入set中，接著不斷往前與往後探索最長的長度，其程式碼如下：


```java
public class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        HashSet<Integer> set = new HashSet<Integer>();
        
        for (int i = 0; i < nums.length; i++) {
            set.add(nums[i]);
        }
        
        int max = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length; i++) {
            if (set.contains(nums[i])) {
                int count = 1;
                int next = nums[i] - 1;
                while (set.contains(next)) {
                    set.remove(next);
                    count++;
                    next--;
                    
                }
                
                next = nums[i] + 1;
                while (set.contains(next)) {
                    set.remove(next);
                    count++;
                    next++;
                    
                }
                max = (count > max) ? count : max;
            }
        }
        return max;
    }
}
```
---
###Reference
1. http://blog.csdn.net/fightforyourdream/article/details/15024861