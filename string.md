# Top K Frequent Words

#### 題目：

[https://leetcode.com/problems/top-k-frequent-words/](https://leetcode.com/problems/top-k-frequent-words/)

#### 題意：

給定一個字串陣列，求其中k個頻率最高的字串。

#### 解法：

##### \[排序\] 

###### 使用一個Map&lt;String, Integer&gt; map 來紀錄各個字串出現的次數，接著再靠出現的次數把key entry排列，最後輸出K個字串，此法最簡單，但是需要 $$O(NlogN)$$時間與 $$O(N)$$的空間複雜度。

```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        Map<String, Integer> count = new HashMap();
        for (String word: words) {
            count.put(word, count.getOrDefault(word, 0) + 1);
        }
        List<String> candidates = new ArrayList(count.keySet());
        Collections.sort(candidates, (w1, w2) -> count.get(w1).equals(count.get(w2)) ?
                w1.compareTo(w2) : count.get(w2) - count.get(w1));

        return candidates.subList(0, k);
    }
}
```

\[Heap\]

多使用一個Heap來輔助來降低整個排序的時間複雜度，此heap以以下兩個條件來排序並不斷的維持k個元素，最後把所有元素輸出到陣列後反轉\(因為此為min heap，需要不斷淘汰出現次數最少的字串\)。

* 字串的出現次數
* 若出現的次數相同，則較短或較前字母的字為先。

此法只需要 $$O(NlogK + K)$$時間與$$O(N + K)$$的空間。

```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        List<String> result = new ArrayList<>();
        if (words == null || words.length == 0 || k == 0) {
            return result;
        }
        
        Map<String, Integer> map = new HashMap<>();
        for (String word : words) {
            map.put(word, map.getOrDefault(word, 0) + 1);
        }
        
        PriorityQueue<String> queue = new PriorityQueue<>(
            (w1, w2) -> {
                if (map.get(w1) == map.get(w2)) {
                    return w2.compareTo(w1);
                } else {
                    return map.get(w1) - map.get(w2);
                }
            }
        );
        
        for (String key : map.keySet()) {
            queue.offer(key);
            if (queue.size() > k) {
                queue.poll();
            }
        }
        
        while (!queue.isEmpty()) {
            result.add(queue.poll());
        }
        
        Collections.reverse(result);
        return result;
        
    }
}  
```



