# Sliding Window Maximum

\(原題網址\)\[[http://www.lintcode.com/en/problem/sliding-window-maximum/](http://www.lintcode.com/en/problem/sliding-window-maximum/)\]

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

維護maxheap的方法，也會超時，除非加入hashheap來幫助加速刪除的動作

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

---

用deque\(雙向隊列\)來解

```java
public ArrayList<Integer> maxSlidingWindow(int[] nums, int k) {

    ArrayList<Integer> res = new ArrayList<Integer>();

    if (nums == null || nums.length == 0) {
        return res;
    }

    // deque 要用arraydeque來實作
    Deque<Integer> deque = new ArrayDeque<Integer>();

    for (int i = 0; i < nums.length; i++) {

        // 把比目前這個數都小的其他數都從後面poll掉，
        // 因為那些數不可能再成為maximum的其中一員
        while(!deque.isEmpty() && nums[i] >deque.peekLast()) {
            deque.pollLast();
        }

        // 把目前最大的poll進來，此時deque可能還有數，但一定比目前這個數大
        deque.offer(nums[i]);

        // 確保超出window範圍的數已被刪除
        if (i > k - 1) {
            if (deque.peekFirst() == nums[i - k]) {
                deque.pollFirst();
            }
        }

        // 此時可以放心把deque的最前面那個peek出來放到答案中
        if (i >= k - 1) {
            res.add(deque.peekFirst());
        }
    }

    return res;
}
```

\[Updated on 2019.10.01\]

##### 解法：

我們可以使用一個Monotonic Queue來實現，最大元素的index在queue的peek，最小的元素的index在queue的tail，deque中放的是index而非數值。

```java
class Solution {
    public int[] maxSlidingWindow(int[] a, int k) {		
	
        if (a == null || k <= 0) {
            return new int[0];
        }

        int length = a.length;
        int[] result = new int[length - k + 1];
        int pos = 0;

        // store index
        Deque<Integer> deque = new ArrayDeque<>();
        for (int i = 0; i < length; i++) {

            // remove numbers out of range k
            while (!deque.isEmpty() && deque.peek() < (i - k + 1)) {
                deque.poll();
            }
            
            // remove smaller numbers in k range as they are useless
            while (!deque.isEmpty() && a[deque.peekLast()] < a[i]) {
                deque.pollLast();
            }

            // deque contains index... result contains content
            deque.offer(i);
            if (i >= k - 1) {
                result[pos++] = a[deque.peek()];
            }
        }
        return result;
    }
}
```



