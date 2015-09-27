#Divide Two Integer

[Lintcode](http://www.lintcode.com/en/problem/divide-two-integers/)

題意：兩數相除，不能使用乘法，只能使用加減法。

解題思路：

暴力法，不斷的拿除數去減被除數，直到被除數比除數小，複雜度是$$(2^{31})$$，我們可以利用位運算加上加減法來幫助我們處理這道題，因為任何數皆可以轉換為二進位的表示法。

我們不斷的拿最接近被除數的 power of 2去減掉被除數，接著再把該power數加到result中，一直不斷這麼作，直到被除數比除數小，此法的複雜度為 $$O(logN)$$

> 需要注意的事我們需要使用 long type，否則

其程式碼如下：

```java
public int divide(int dividend, int divisor) {
    
    // 因不能除以0
    if (divisor == 0) {
        return 0;
    }
    // 先轉正整數來處理，之後再轉回來
    long p = Math.abs((long)dividend);
    long q = Math.abs((long)divisor);
    
    int result = 0;
    while ( p >= q) {
        int count = 0;
        while (p >= (p << count)) {
            count++;
        }
        
        result += 1 << (count - 1);
        p -= q << (count - 1);
    }
    
    if ((dividend < 0 && divisor < 0) || (dividend > 0 && divisor > 0)) {
        return result;
    } else {
        return -result;
    }
   
}
```


---
###Reference
1. http://www.cnblogs.com/yuzhangcmu/p/4049170.html