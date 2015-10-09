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

