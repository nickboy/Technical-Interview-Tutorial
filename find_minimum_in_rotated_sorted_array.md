# Find Minimum in Rotated Sorted Array

[原題網址](http://www.lintcode.com/en/problem/find-minimum-in-rotated-sorted-array/)
```java
public int findMin(int[] nums) {
        // write your code here
        if (nums.length == 0) {
            return 0;
        }
        int start = 0;
        int end = nums.length - 1;
        int mid;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            //拿end與mid比
            //若mid比end小，代表最小在左半邊，移動end
            //若mid比end大，代表最小在右半邊，移動start
            if (nums[mid] < nums[end]) {
                end = mid;
            } else {
                start = mid;
            }
        }
        //最後剩兩個數，直接比較
        if (nums[start] < nums[end]) {
            return nums[start];
        } else {
            return nums[end];
        }
    }
```
