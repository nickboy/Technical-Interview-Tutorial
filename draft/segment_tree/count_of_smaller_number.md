#Count of Smaller Number

[原題連結](http://www.lintcode.com/en/problem/count-of-smaller-number/)

題意：給予兩個陣列 A 與 Queries，根據 Queries 陣列中的每個元素，去找出 A 中比 Queries[i] 小的元素個素有幾個。

解法：此題可有三個解法，
1. 兩層循環，複雜度高
2. 排序後再一次遍歷
3. 線段樹

## 兩層循環解法

```java
public ArrayList<Integer> countOfSmallerNumber(int[] A, int[] queries) {
    
    ArrayList<Integer> res = new ArrayList<Integer>();
    
    if (A == null ||  queries == null || queries.length == 0) {
        return res;
    }
    
    for (int i = 0; i < queries.length; i++) {
        int count = 0;
        for (int j = 0; j < A.length; j++) {
            if (queries[i] > A[j]) {
                count++;
            }
        }
        res.add(count);
    }
    
    return res;
}
```

>時間複雜度：O(n^2)