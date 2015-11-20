# Search in Rotated Sorted Array II

[Leetcode](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)

題意：

Follow up for "Search in Rotated Sorted Array":
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?

Write a function to determine if a given target is in the array.


解題思路：

九章模版，差別在於，如果有遇到重複的，則直接start往前移。

```java
public class Solution {
    public boolean search(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return false;
        }
        
        int start = 0;
        int end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[start] < nums[mid]) {
                if (nums[start] <= target && nums[mid] > target) {
                    end = mid;
                } else {
                    start = mid;
                }
            } else if (nums[start] > nums[mid]){
                if (nums[mid] < target && nums[end] >= target) {
                    start = mid;
                } else {
                    end = mid;
                }
            } else {
                start++;
            }
        }
        
        if (nums[start] == target) {
            return true;
        } else if (nums[end] == target) {
            return true;
        } else {
            return false;
        }
    }
}
```