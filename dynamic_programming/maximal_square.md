#Maximal Square

[]()

題意：

Given an array of integers and a number k, find k non-overlapping subarrays which have the largest sum.

The number in each subarray should be contiguous.

Return the largest sum.

**Example**

Given $$[-1,4,-2,3,-2,3]$$, $$k=2$$, return $$8$$

**Note**

The subarray should contain at least one number

解題思路：

暴力法：枚舉陣列中的每個元素當矩型的左上元素，不斷的向右下延伸，解法只過了三個case，待發現錯誤再回頭修正。

```java
public int maxSquare(int[][] matrix) {
    
    if (matrix == null || matrix.length == 0) {
        return 0;
    }
    
    int length = matrix.length;
    int width = matrix[0].length;
    int res = 0;
    
    for (int i = 0; i < length; i++) {
        for (int j = 0; j < width ;j++) {
            
            if (matrix[i][j] == 0) {
                continue;
            } else {
                res = (res > 1) ? res : 1;
            }
            
            int innerLength = i;
            int innerWidth = j;
            while (innerLength + 1 < length && innerWidth + 1 < width) {
                
                int left = matrix[innerLength][innerWidth + 1];
                int bottom = matrix[innerLength + 1][innerWidth];
                int leftBottom = matrix[innerLength + 1][innerWidth + 1];
                
                if (left == 1 && bottom == 1 && leftBottom == 1) {
                    
                    innerLength++;
                    innerWidth++;
                    int area = (innerLength - length ) * (innerWidth - width);
                    if (area > res) {
                        res = area;
                    }
                } else {
                    break;
                }
            }
        }
    }
    
    return res;
}
```
