#Building Outline

[原題網址](http://www.lintcode.com/en/problem/building-outline/)


解題思路：

根據 [網友](https://codesolutiony.wordpress.com/2015/06/01/leetcode-the-skyline-problem-lintcode-building-outline/) 提供以下思路：

把每一個building拆成兩個edge，一個入一個出。所有的edge加入到一個list中。再對這個list進行排序。

**排序順序為：如果兩個邊的position不一樣，那麼按pos排，否則根據edge是入還是出來排。**

根據position從前到後掃瞄每一個edge，將edge根據是入還是出來將當前height加入或者移除heap。再得到當前最高點來決定是否加入最終結果。非常巧妙，值得思考。



---
###Reference
1. https://codesolutiony.wordpress.com/2015/06/01/leetcode-the-skyline-problem-lintcode-building-outline/