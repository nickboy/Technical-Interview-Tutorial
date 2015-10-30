# Sudoku Solver

[Leetcode](https://leetcode.com/problems/sudoku-solver/)

題意：給一個數獨，寫程式解開它

解題思路：

其實跟解n queen一樣，每放入一個合法的格，再往下一格寫，直到解完整個數獨，在這裡使用true false來判所是否這條路可行，若不可行，則不繼續往下走。

```java
public class Solution {
    public void solveSudoku(char[][] board) {
        if (board == null || board.length != 9 || board[0].length != 9) {
            return;
        }
        helper(board, 0, 0);
    }
    
    public boolean helper(char[][] board, int i, int j) {
        
        // 已走到列的盡頭，繼續往下新的一列
        if (j >= 9) {
            return helper(board, i + 1, 0);
        }
        
        // 已完成整個填表動作
        if (i == 9) {
            return true;
        }
        
        // 當格子為'.'時才要去作填表動作
        if (board[i][j] == '.') {
            for (int k = 1; k <= 9; k++) {
                board[i][j] = (char)(k + '0');
                if (isValid(board, i, j)) {
                    if (helper(board, i, j + 1)) {
                        return true; // 找到對的答案要即時return，不能再變回'.'
                    }
                }
                board[i][j] = '.';
            }
        } else {
            return helper(board,i, j + 1); // 記得作return動作，不return的話，上一層不知道你是對是錯，會把那格又改回'.'了。
        }
        return false;
    }
    
    private boolean isValid(char[][] board, int x, int y) {
        // check column
        for (int i = 0; i < 9; i++) {
            if (i != x && board[i][y] == board[x][y]) {
                return false;
            }
        }
        // check row
        for (int i = 0; i < 9; i++) {
            if (i != y && board[x][i] == board[x][y]) {
                return false;
            }
        }
        // check block
        for (int row = x / 3 * 3; row < x / 3 * 3 + 3; row++) {
            for (int col = y / 3 * 3; col < y / 3 * 3 + 3; col++) {
                if ((row != x || col != y) && board[row][col] == board[x][y]) {
                    return false;
                }
            }
        }
        
        return true;
    }
}
```

---
###Reference
1. http://blog.csdn.net/linhuanmars/article/details/20748761