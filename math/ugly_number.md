#Ugly Number

[原題網址](https://leetcode.com/problems/ugly-number/)

題意：

Ugly Number的定義，他的 facto 只能夠是 3，5，7。

給定一個數 n ，判斷該數是否為 ugly number

解題思路：

使用遞回去作，一方面判斷 n 除以 3 5 7 的餘數是否為0 ，若是的話，則繼續往下判斷，其程式碼如下：

```java
public boolean isUgly(int n) {
    if (n < 1)
        return false;
    if (n == 1)
        return true;
        
    return ((n % 2 == 0) && isUgly(n / 2)) ||
            ((n % 3 == 0) && isUgly(n / 3)) ||
            ((n % 5 == 0) && isUgly(n / 5));
}
```

