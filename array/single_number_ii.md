# Single Number II

[原題連結](http://www.lintcode.com/en/problem/single-number-ii/)

題意：此為 [Single Number](array/single_number.md) 的變形，此時每個元素皆出現三次，只有一個元素出現一次，找出那個元素。

解題思路：這一題就無法用上一題的 XOR 解法，因每個元素皆出現三次，但我們可以自己實作三進制，搭配上不進位加法來模擬三進制的 XOR 。

作法：
+ 把每個數轉成三進制
+ 接著用不進位加法
+ 再轉回十進制

程式碼如下：

```java
public int singleNumberII(int[] A) {
    if (A == null || A.length == 0) {
        return -1;
    }
    
    // get the power of 3
    int[] pow3 = new int[20];
    pow3[0] = 1;
    for (int i = 1; i < 20; i++) {
        pow3[i] = pow3[i - 1] * 3;
    }
    
    // at most 20 bits for base 3 in maxint
    int[] bits = new int[20]; 
    
    for (int i = 0; i < 20; i++) {
        for (int j = 0; j < A.length; j++) {
            bits[i] += A[j] / pow3[i] % 3;
        }
    }
    
    // convert to decimal
    int result = 0;
    for (int i = 0; i < 20; i++) {
        result += pow3[i] * (bits[i] % 3);
    }
    return result;
}
```
