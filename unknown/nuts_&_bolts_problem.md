# Nuts & Bolts Problem

[Lintcode](http://www.lintcode.com/en/problem/nuts-bolts-problem/)

題意：



解題思路：

引用網友 [mnmunknown](http://www.1point3acres.com/bbs/forum.php?mod=viewthread&action=printable&tid=138798) 的思路如下

"基本思路很簡單，由於 compare 規定只能按（nut, bolt）的順序放， 先從 nut 裡選一個做 pivot ，按此 pivot 與 bolts array 進行比較並且進行 partition ; 而後返回 pivot element 的 index ，代表對應原先選擇的 nut 的 bolt ，並且以此元素回到 nuts array 裡面進行 partition ； 最後遞歸處理左右兩邊。"

