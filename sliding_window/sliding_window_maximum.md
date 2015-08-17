#Sliding Window Maximum


(原題網址)[http://www.lintcode.com/en/problem/sliding-window-maximum/]

題意：找出window內的最大值

暴力法：會超時

```java
public ArrayList<Integer> maxSlidingWindow(int[] nums, int k) {
        
    ArrayList<Integer> res = new ArrayList<Integer>();
    
    if (nums == null || nums.length == 0) {
        return res;
    }
    
    for (int i = 0; i <= nums.length - k; i++) {
        int max = nums[i];
        for (int j = i; j <= i + k - 1; j++) {
            if (max < nums[j]) {
                max = nums[j];
            }
        }
        res.add(max);
    }
    
    return res;
}
```
---
維護maxheap的方法，也會超時

```java
public ArrayList<Integer> maxSlidingWindow(int[] nums, int k) {
        
    ArrayList<Integer> res = new ArrayList<Integer>();
    
    if (nums == null || nums.length == 0) {
        return res;
    }
    
    PriorityQueue<Integer> maxHeap = new PriorityQueue<Integer>(1, Collections.reverseOrder());
    
    for (int i = 0; i < nums.length; i++) {
        maxHeap.offer(nums[i]);
        
        if (i >= k - 1) {
            res.add(maxHeap.peek());
            
            int toBeDelete = nums[i - k + 1];
            maxHeap.remove(toBeDelete);
        }
    }
    
    return res;
}
```