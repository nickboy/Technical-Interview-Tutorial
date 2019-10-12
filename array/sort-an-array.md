# Sort an Array

##### 題目連結：[https://leetcode.com/problems/sort-an-array/](https://leetcode.com/problems/sort-an-array/)

##### 題意：排序一個陣列

解題思路：

\[Quick Sort\] 

利用Divide and Conquer 的方來作排序，每次挑一個pivot值，將比pivot值小的所有元素放在pivot的左邊，比pivot值大的所有元素放在pivot的右邊，接著再將兩邊分邊再細分作排序。

```java
class Solution {
    public Random rand;
    public int[] sortArray(int[] nums) {
        rand = new Random();
        quickSort(nums, 0, nums.length - 1);
        return nums;
    }
    
    private void quickSort(int[] nums, int start, int end) {
        if (start >= end) return;
        
        int index = rand.nextInt(end - start + 1) + start;
        int pivot = nums[index];
        int left = start;
        int right = end;
        
        while (left <= right) {
            while (left <= right && nums[left] < pivot)
                left++;
            while (left <= right && nums[right] > pivot) 
                right--;
            
            if (left <= right) {
                swap(nums, left, right);
                left++;
                right--;
            }
        }
        
        quickSort(nums, start, right);
        quickSort(nums, left, end);
    }
    
    private void swap(int[] nums, int one, int two) {
        int temp = nums[one];
        nums[one] = nums[two];
        nums[two] = temp;
    }
}
```

\[Merge Sort\] 

也是利用Divide and Conquer，不斷將陣列對半分，再將sort好的兩個局部結果合併。

```js
class Solution {
    public int[] sortArray(int[] nums) {
        int[] temp = new int[nums.length];
        mergeSort(nums, 0, nums.length - 1, temp);
        return nums;
    }
    
    public void mergeSort(int[] nums, int start, int end, int[] temp) {
        if (start >= end) 
            return;
        int left = start;
        int right = end;
        int mid = start + (end - start) / 2;
        mergeSort(nums, start, mid, temp);
        mergeSort(nums, mid + 1, end, temp);
        merge(nums, start, mid, end, temp);
    }
    
    private void merge(int[] nums, int start, int mid, int end, int[] temp) {
        int left = start;
        int right = mid + 1;
        int index = start;
        while (left <= mid && right <= end) {
            if (nums[left] < nums[right]) {
                temp[index++] = nums[left++];
            } else {
                temp[index++] = nums[right++];
            }
        }
        
        while (left <= mid) {
            temp[index++] = nums[left++];
        }
        
        while (right <= end) {
            temp[index++] = nums[right++];
        }
        
        for (index = start; index <= end; index++) {
            nums[index] = temp[index];
        }
    }
    
    
}
```

##### Reference:

* [https://www.youtube.com/watch?v=qr1W-eHgJVg](https://www.youtube.com/watch?v=qr1W-eHgJVg)

* [https://www.youtube.com/watch?v=rFwuRK4\_TNQ](https://www.youtube.com/watch?v=rFwuRK4_TNQ)



