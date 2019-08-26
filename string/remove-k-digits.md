# Remove K Digits

[https://leetcode.com/problems/remove-k-digits/](https://leetcode.com/problems/remove-k-digits/)

**題意：**

Given a non-negative integer _num_ represented as a string, remove _k_ digits from the number so that the new number is the smallest possible.

  
**解題思路：**

這是一個典型的greedy algorithm，我們需要刪除的字就是字串中的peak數字，我們一旦找到了字串中的峰值，刪除即可，通常處理這類的情況，我們會使用Stack，不斷的維持Stack中的數字是遞增的形式，一旦發現peek\(\)的數比當下的數還大時，不斷pop，最後再將當下的數字放入Stack，最後將Stack的數字pop出來再作reverse即可，但需要處理leading zero的情況。



**解法：**

```java
public class Solution {
    public String removeKdigits(String num, int k) {
        int digits = num.length() - k;
        char[] stk = new char[num.length()];
        int top = 0;
        // k keeps track of how many characters we can remove
        // if the previous character in stk is larger than the current one
        // then removing it will get a smaller number
        // but we can only do so when k is larger than 0
        for (int i = 0; i < num.length(); ++i) {
            char c = num.charAt(i);
            while (top > 0 && stk[top-1] > c && k > 0) {
                top -= 1;
                k -= 1;
            }
            stk[top++] = c;
        }
        // find the index of first non-zero digit
        int idx = 0;
        while (idx < digits && stk[idx] == '0') idx++;
        return idx == digits? "0": new String(stk, idx, digits - idx);
    }
}
```

**Reference: **

* [https://leetcode.com/problems/remove-k-digits/discuss/88660/A-greedy-method-using-stack-O\(n\)-time-and-O\(n\)-space](https://leetcode.com/problems/remove-k-digits/discuss/88660/A-greedy-method-using-stack-O%28n%29-time-and-O%28n%29-space)



