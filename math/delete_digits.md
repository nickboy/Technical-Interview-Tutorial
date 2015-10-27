# Delete DIgits

[Lintcode](http://www.lintcode.com/en/problem/delete-digits/)

題意：



解題思路：


以下引用網友 [Edward Liu](http://www.cnblogs.com/EdwardLiu/p/4276260.html) 的解說：

找第一個遞減的位置所在。那道題是想要改動的影響最小，所以從右邊開始掃瞄。這道題是想要改動的影響最大，所以從左邊開始掃瞄。

這道題，刪掉一個數，相當於用這個數後面的數代替這個數。所以後面這個數一定要比當前小才行。所以找的是第一個遞減的位置，把大的那個數刪了。

這樣做一次就是找到了：刪除哪一個數，使得剩下的數最小。對剩下的數再做k次，就可以找到刪除哪k個數，使得剩下的數最小。這其實是一個Greedy算法，因為這樣每做一次，得到的都是當前最優的結果。

自己的小叮嚀：

>需要注意leading zero的問題，如100000614，依我們的演算法會刪除第一個1，變成00000614，要先把 leading zeros刪除掉再作後續處理。並且注意邊界的處理


```java
public class Solution {
    /**
     *@param A: A positive integer which has N digits, A is a string.
     *@param k: Remove k digits.
     *@return: A string
     */
    public String DeleteDigits(String A, int k) {
        if (A == null || A.length() == 0 || k == 0) {
            return A;
        }
        if (k == A.length()) {
            return "";
        }
        
        StringBuilder res = new StringBuilder(A);
        for (int i = 1; i <= k; i++) {
            int j;
            for (j = 0; j < res.length() - 1; j++) {
                    int cur = (int)res.charAt(j) - '0';
                    int next = (int)res.charAt(j + 1) - '0';
                    if (cur > next) {
                        break;
                    } 
            }
            res.deleteCharAt(j);
            
            // remove leading zeros
            int l = 0;
            while (l < res.length() && res.charAt(l) == '0'){
                res.deleteCharAt(l);
                l++;
            }
        }
        
        
        
        return res.toString();
        
    }
}

```

看起來需要O(Nk)時間複雜度，但其實用一個Stack，再記錄pop了幾次，O(2N)就好了




---
###Reference
1. http://www.cnblogs.com/EdwardLiu/p/4276260.html