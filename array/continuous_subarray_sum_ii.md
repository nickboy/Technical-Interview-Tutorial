#Continuous Subarray Sum II

[原題網址](http://www.lintcode.com/en/problem/continuous-subarray-sum-ii/)

題意：與 I 相同，但這次陣列可以旋轉。

Give ```[3, 1, -100, -3, 4]```, return ```[4,1]```.

解題思路：

網友 stellari 提供以下思路：

最大數組的範圍只有兩種可能：
1. [ i ~ j ]
2. [ i ~ N-1] + [ 0 ~ j ]. 

所以，你只要分別找到兩種情況的最大者，取這兩個最大者中較大的即可。

1和Continuous Subarray Sum I相同，就不多說了。

2等價於找一個範圍[j+1 ~i-1]，使得這個範圍內的數組和最小。這又等價於將原數組取負號，然後在這個負數組中找最大和的[j+1 ~ i+1]範圍即可。


網友 momocoisapeach 亦提供以下思路：

思路是這樣的，像樓上說的兩種情況，不rotate的 和rorate的。不rotate的和Continuous Subarray Sum I做法一樣，不說了。rotate的，可以這樣想，rotate的結果其實相當於是把原來的array中間挖了一段連續的array，那麼挖哪一段呢？肯定是和最小的一段連續array。這樣解法就出來了。" Y, r, p3 }. a
類似Continuous Subarray Sum I，在I裡面是找到連續和最大的一段subarray，在這裡，不僅找到和最大的一段連續array，並且也找到和最小的一段連續array，然後用整個array的sum減去這個最小的和，如果大於不rotate的最大和，那麼解就是挖去的這段array的（尾+1， 頭-1）6 t" C' P% I& `8 D


---
###Reference
1. http://www.1point3acres.com/bbs/forum.php?mod=viewthread&action=printable&tid=137556