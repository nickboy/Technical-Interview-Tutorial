# Gas Station

[Lintcode](http://www.lintcode.com/en/problem/gas-station/)

題意：

There are N gas stations along a circular route, where the amount of gas at station i is ```gas[i]```.

You have a car with an unlimited gas tank and it costs ```cost[i]``` of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

Example

Given 4 gas stations with ```gas[i]=[1,1,3,1]```, and the ```cost[i]=[2,2,1,1]```. The starting gas station's index is ```2```.

Note
The solution is guaranteed to be unique.

Challenge
O(n) time and O(1) extra space

解題思路：

>由於此題只需要找出是否有可能的解，並回傳起始的index，因此我們只需要檢查所有 diff是否為正，若為正，則回傳該 startIndex。

引自 [Lexi](https://leetcodenotes.wordpress.com/2013/11/21/leetcode-gas-station-%E8%BD%AC%E5%9C%88%E7%9A%84%E5%8A%A0%E6%B2%B9%E7%AB%99%E7%9C%8B%E8%83%BD%E4%B8%8D%E8%83%BD%E8%B5%B0%E4%B8%80%E5%9C%88/) 網友的解答：

1. 從i開始，j是當前station的指針，sum += gas[j] – cost[j] （從j站加了油，再算上從i開始走到j剩的油，走到j+1站還能剩下多少油）
2. 如果sum < 0，說明從i開始是不行的。那能不能從i..j中間的某個位置開始呢？既然i出發到i+1是可行的， 又i~j是不可行的， 從而發現i+1~ j是不可行的。
3. 以此類推i+2~j， i+3~j，i+4~j 。。。。等等都是不可行的
4. 所以一旦sum<0，index就賦成j + 1，sum歸零。
5. 最後total表示能不能走一圈。


```java
public class Solution {
    /**
     * @param gas: an array of integers
     * @param cost: an array of integers
     * @return: an integer
     */
    public int canCompleteCircuit(int[] gas, int[] cost) {
        
        if (gas == null || gas.length == 0 || cost == null || cost.length == 0) {
            return -1;
        }
        
        int len = cost.length;
        int total = 0; // 累積整個環的所有差值，如果結果為負的話，代表找不到任何結果
        int sum = 0; // 指從j站加了油，再算上從i開始走到j剩的油，走到j+1站還能剩下多少油
        int startIndex = 0; // 指從哪裡開始走
        
        for (int i = 0; i < len; i++) {
            int diff = gas[i] - cost[i];
            sum += diff;
            if (sum < 0) {
                // 表示從第0個加油站到目前這個加油站沒有解答
                // 因此從下一個加油站開始繼續找。
                startIndex = i + 1;
                sum = 0;
            }
            total += diff;
        }
        
        // total是否為正，若為負則表示沒有任何答案，返回-1，否則返回startindex
        if (total < 0) {
            return -1;
        } else {
            return startIndex;
        }
    }
}
```

---
###Reference
1. http://www.cnblogs.com/yuzhangcmu/p/4179228.html
2. https://leetcodenotes.wordpress.com/2013/11/21/leetcode-gas-station-%E8%BD%AC%E5%9C%88%E7%9A%84%E5%8A%A0%E6%B2%B9%E7%AB%99%E7%9C%8B%E8%83%BD%E4%B8%8D%E8%83%BD%E8%B5%B0%E4%B8%80%E5%9C%88/