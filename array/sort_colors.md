# Sort Colors
[原題網址](http://www.lintcode.com/en/problem/sort-colors/)

```java
class Solution {

    public void sortColors(int[] nums) {
        if (nums == null || nums.length == 0) {
            return;
        }
        int left = 0;
        int right = nums.length - 1;
        int point = 0;
        // 利用三個指針，left, right, point
        // left負責0，point負責1，right負責2
        while (point <= right) {

            if (nums[point] == 0) {
                swap(nums, left, point);
                left++;
                point++;
            } else if (nums[point] == 1) {
                point++;
            } else {
                swap(nums, point, right);
                right--; //只移動right，因可能當下right指向的值也是2，要在下一輪繼續處理

            }
        }
    }

    private void swap(int[] A, int idxA, int idxB) {
        int temp = A[idxA];
        A[idxA] = A[idxB];
        A[idxB] = temp;
    }
}

```
