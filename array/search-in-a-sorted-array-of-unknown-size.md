# Search in a Sorted Array of Unknown Size

[Leetcode](https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/)

#### 題解：

由於不知道陣列的大小，我們可以使用類似Expernential backoff方法，從陣列的第一個開始找，如果還是比target小的話，往第二個找，接著第四個，每次index乘以2，當比對的值比target大時，開始使用binary search來搜。



```java
class Solution {
    public int search(ArrayReader reader, int target) {
        
        int count = 1;
        
        while (reader.get(count) < target) {
            count = count * 2;
        }
        
        int start = count / 2;
        int end = count;
        
        while ( start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (reader.get(mid) < target) {
                start = mid;
            } else {
                end = mid;
            } 
        }
        
        if (reader.get(start) == target) {
            return start;
        }
        
        if (reader.get(end) == target) {
            return end; 
        }
        
        return -1;
    }
}
```



