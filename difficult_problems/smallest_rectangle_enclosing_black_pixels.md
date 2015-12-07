# Smallest Rectangle Enclosing Black Pixels

[Leetcode](https://leetcode.com/problems/smallest-rectangle-enclosing-black-pixels/)

題意：

An image is represented by a binary matrix with 0 as a white pixel and 1 as a black pixel. The black pixels are connected, i.e., there is only one black region. Pixels are connected horizontally and vertically. Given the location (x, y) of one of the black pixels, return the area of the smallest (axis-aligned) rectangle that encloses all black pixels.

For example, given the following image:
```
[
  "0010",
  "0110",
  "0100"
]
```
and x = 0, y = 2,
Return 6.



解題思路：

主要是作以下的事情

>- top = search row [0...x], find first row contain 1,
- bottom = search row[x+1, row], find first row contian all 0
- left = search col[0...y], find first col contain 1,
- right = search col[y+1, col], find first col contain all 0
- return (right - left) * (bottom - top)




---
###Reference
1. https://leetcode.com/problems/smallest-rectangle-enclosing-black-pixels/