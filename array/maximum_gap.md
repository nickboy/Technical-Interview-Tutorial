# Maximum Gap

[Leetcode](https://leetcode.com/problems/maximum-gap/)

題意：

解題思路：

暴力法花 O(NlogN) 排序後再不斷跟前面的值比對，程式碼如下：

```java
public class Solution {
    public int maximumGap(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        Arrays.sort(nums);
        int maxGap = 0;
        for (int i = 1; i < nums.length; i++) {
            if ((nums[i] - nums[i - 1]) > maxGap) {
                maxGap = nums[i] - nums[i - 1];
            }
        }
        return maxGap;
    }
}
```

O(N) 的解法，利用桶排序，以下為 leetcode官網的解法：

Suppose there are N elements and they range from A to B.

Then the maximum gap will be no smaller than ceiling[(B - A) / (N - 1)]

Let the length of a bucket to be len = ceiling[(B - A) / (N - 1)], then we will have at most num = (B - A) / len + 1 of bucket

for any number K in the array, we can easily find out which bucket it belongs by calculating loc = (K - A) / len and therefore maintain the maximum and minimum elements in each bucket.

Since the maximum difference between elements in the same buckets will be at most len - 1, so the final answer will not be taken from two elements in the same buckets.

For each non-empty buckets p, find the next non-empty buckets q, then q.min - p.max could be the potential answer to the question. Return the maximum of all those values.