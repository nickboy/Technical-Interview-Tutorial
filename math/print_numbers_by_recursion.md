#Print Numbers by Recursion

[原題網址](http://www.lintcode.com/en/problem/print-numbers-by-recursion/)

題意：給一個數 n 代表位數，印出所有小於該位數的所有數字。

Print numbers from 1 to the largest number with N digits by recursion.

Example

Given N = 1, return ```[1,2,3,4,5,6,7,8,9]```.

Given N = 2, return ```[1,2,3,4,5,6,7,8,9,10,11,12,...,99]```.

解題思路：

暴力法：

```java
public class Solution {
    /**
     * @param n: An integer.
     * return : An array storing 1 to the largest number with n digits.
     */
    public List<Integer> numbersByRecursion(int n) {
        
        int digits = 10;
        for (int i = 1; i < n; i++) {
            digits *= 10;
        }
        
        List<Integer> res = new ArrayList<Integer>();
        if (n == 0) {
            return res;
        }
        
        helper(1, digits, res);
        return res;
    }
    
    public void helper(int i, int digits, List<Integer> res) {
        if (i >= digits) {
            return;
        }
        res.add(i);
        helper(i + 1, digits, res);
    }
}

```

