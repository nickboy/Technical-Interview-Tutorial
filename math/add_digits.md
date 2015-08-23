#Add Digits

[原題連結](https://leetcode.com/problems/add-digits/)

題意：

Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

For example:

Given ```num = 38```, the process is like: ```3 + 8 = 11, 1 + 1 = 2```. Since 2 has only one digit, return it.

Follow up:
Could you do it without any loop/recursion in $$O(1)$$ runtime?

解法一(循環)，程式碼如下：

```java
public int addDigits(int num) {
    
    if (num < 10) {
        return num;
    }
    
    while (num >= 10) {
        int temp = num;
        int result = 0;
        while (temp > 0) {
            result += temp % 10;
            temp /= 10;
        }
        
        num = result;
    }
    
    return num;
}
```
> Time Complexity：待分解

---
另有$$O(1)$$的解法，假設有一數 100a+10b+c, then (100a+10b+c)%9=(a+99a+b+9b+c)%9=(a+b+c)%9


```java
public int addDigits2(int num) {
    
    if (num < 10) {
        return num;
    }
    
    return (num % 9 != 0) ? num % 9 : 9;
}
```

> Time Complexity：$$O(1)$$