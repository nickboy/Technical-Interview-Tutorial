# Word Ladder II

[Lintcode]()

題意：

與[Word Ladder I](unknown/word_ladder_i.md)一樣，但不同的是要找出所有可能的最優解路徑

解題思路：

網友 [JustDoIT](http://www.cnblogs.com/TenosDoIt/p/3443512.html) 提供了以下思路，我再自己整理了一下：

一樣使用廣度搜尋來解，但是我們有兩個問題需要解決

1. 怎樣保證求得所有的最優解
2. 怎麼構造路徑


關於第一個問題
* 我們不能直接找到相鄰的單詞就把它從dict中移掉，因為上一層的其他單詞可能也可以走到這個字。
* 走完當前程時，也需要把所有相鄰的字從dict中刪除，否則還是會有cycle，在此我們使用一個hashmap來保證加入queue中的單詞不會重複，hashmap在每層歷遍後即清空
* 一但找到單詞等於end時，就停止繼續往下找，因為就算再繼續往下找，長度一定會超出最優解的。
* 

關於第二個問題：
* 為了輸出所有最短的路徑，我們可以在bfs時保存每個節點的father，因每個節點可能有多條路可到達，即有多個father，因此hasmap的value即是一個list來保存所有可能的father。
* 遞迴來建path會使程式碼較簡潔。
* 




---
###Reference
1. http://bangbingsyb.blogspot.com/2014/11/leetcode-word-ladder-i-ii.html
2. http://blog.csdn.net/niaokedaoren/article/details/8884938
3. http://rangerway.com/way/leetcode-word-ladder-ii/
4. http://www.1point3acres.com/bbs/thread-51646-1-1.html
