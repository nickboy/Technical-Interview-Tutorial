#Product of Array Exclude itself

[原題連結](http://www.lintcode.com/en/problem/product-of-array-exclude-itself/)

題意：算出陣列的總積除了當下的那個元素i，不能使用除法。


Given an integers array A.

Define ```B[i] = A[0] * ... * A[i-1] * A[i+1] * ... * A[n-1]```, calculate B WITHOUT divide operation.

For ```A = [1, 2, 3]```, return ```[6, 3, 2]```.


解題思路：分別用兩個陣列 left 與 right 
+ left[i] 紀錄從0乘到 i - 1 的總積
+ right[i] 紀錄從 i + 1 乘到 len - 1的總積
+ left[i] * right[i] 代表從頭乘到尾但排除A[i]
+ 此方式需要花 $$O(2N)$$的空間複雜度

程式碼如下：

```java
public ArrayList<Long> productExcludeItself(ArrayList<Integer> A) {
    
    ArrayList<Long> res = new ArrayList<Long>();
    
    if (A == null || A.size() == 0) {
        return res;
    }
    
    // 利用left與right的兩個陣列
    // left[i]代表從A[0] * ... * A[i-1]的積
    // right[i] 代表從A[i+1] * ... * A[len - 1]的積
    int len = A.size();
    long[] left = new long[len];
    long[] right = new long[len];
    long productLeft = 1;
    long productRight = 1;
    
    for (int i = 0; i < len; i++) {
        productLeft *= (i > 0) ? A.get(i-1) : 1;
        left[i] = productLeft;
        productRight *= (i > 0) ? A.get(len - i) : 1;
        right[len - i - 1] = productRight;
    }
    
    // left[i] * right[i] 代表整個整陣的總積除了第i個元素外
    for (int i = 0; i < len; i++) {
        res.add(left[i] * right[i]);
    }
    
    return res;
    
}
```

---
另有一 $$O(1)$$ 空間複雜度的作法
