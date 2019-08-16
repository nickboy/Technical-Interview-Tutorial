# Task Scheduler

#### 題意：

給一段**characters**與一個整數**N**，characters代表是所有task要丟到CPU裡去跑，且N代表每跑N個cycle時，CPU需要休息一下，必須找出一個跑法是需要最少的cycle數。

#### 解法：

能想到的就是貪心\(Greedy\)解法，希望能先把耗費最多cycle數的task先跑完，我們可以先跑一次把各個task所需的cycle數計算出來，接著使用一個MaxHeap來不斷維護當下最多cycle的task，由於我們不需要印出來跑的順序，因此只要維護剩下的cycle數即可。

> 這題沒有考慮到context switch的成本，因此任務之間交互跑是沒問題的，只要確保能把耗費最多cycle數的任務先跑完即可。



```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        Map<Character, Integer> map = new HashMap<>();
        PriorityQueue<Integer> queue = new PriorityQueue<>((a, b) -> b - a);
        
        for (char c : tasks) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        queue.addAll(map.values()); 
        
        int cycle = 0;
        while (!queue.isEmpty()) {
            List<Integer> list = new ArrayList<>();
            for (int i = 0; i <= n; i++) {
                if (!queue.isEmpty()) {
                    list.add(queue.remove());
                }
            }
            
            for (int val : list) {
                if (--val > 0) {
                    queue.offer(val);
                }
            }
            // 如何queue已空，則只需要加上當下耗費多少cycle，如果還未空，則需加上idle cycle與當下花了總共多少cycles。
            cycle += (queue.isEmpty()) ? list.size() : n + 1;
        }
        
        return cycle;
    }
}
```

#### Reference:

* [https://leetcode.com/problems/task-scheduler/](https://leetcode.com/problems/task-scheduler/)
* [https://www.youtube.com/watch?v=ySTQCRya6B0](https://www.youtube.com/watch?v=ySTQCRya6B0)





