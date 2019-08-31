# Armstrong Number

#### 題目：

#### [https://leetcode.com/problems/armstrong-number/](https://leetcode.com/problems/armstrong-number/)

#### 解題思路：

首先算出數字的長度，接著不斷用mod去取最後一位數並不斷加總，最後驗證sum是否等於N



```java
class Solution {
    public boolean isArmstrong(int N) {
        if (N == 0) {
            return true;
        }
        
        int len = 0;
        int copyN = N;
        while (copyN > 0) {
            len++;
            copyN /= 10;
        }
        
        copyN = N;
        int sum = 0;
        while (copyN > 0) {
            int digit = copyN % 10;
            sum += power(digit, len);
            copyN /= 10;
        }
        
        return sum == N;
    }
    
    public int power(int digit, int k) {
        int sum = digit;
        for (int i = 1; i < k; i++) {
            sum *= digit;
        }
        return sum;
    }
}
```



