# Construct Binary Tree from Preorder and Inorder Traversal

[原題網址](http://www.lintcode.com/en/problem/construct-binary-tree-from-preorder-and-inorder-traversal/)

> Given preorder and inorder traversal of a tree, construct the binary tree.

> 給你一顆二元樹的前序遍歷和後續遍歷，要把原本的樹重新構建出來。

這道題無法直接拿出筆畫圖想一個完美的規律。解題關鍵在於善加利用中序遍歷帶來的優勢。回想中序遍歷在任一節點上的定義：`左子樹 -> 節點 -> 右子樹`，可以發現