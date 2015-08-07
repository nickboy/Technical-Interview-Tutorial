#Recover Rotated Sorted Array

```java
public class Solution {
    public void recoverRotatedSortedArray(ArrayList<Integer> nums) {
        // write your code
        int pos = 0;
        for (int i = 0; i < nums.size() - 1; i++) {
            if (nums.get(i) > nums.get(i+1)) {
                pos = i;
                break;
            }
        }
        // 避免sorted array
        // 反轉前半段
        // 反轉後半段
        // 整個反轉
        if (pos != 0) {
            reverseArray(nums, 0, pos);
            reverseArray(nums, pos + 1, nums.size() - 1);
            reverseArray(nums, 0, nums.size() - 1);
        }
    }
    
    
    public void reverseArray(ArrayList<Integer> nums, int start, int end) {
        while (start < end) {
            Collections.swap(nums, start, end);
            start++;
            end--;
        }
    }
}
```