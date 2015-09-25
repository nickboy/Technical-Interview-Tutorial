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