# Game of Life

[]()

題意：

According to the Wikipedia's article: "**The Game of Life**, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

Given a board with m by n cells, each cell has an initial state **live (1) or dead (0)**. Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

1. Any live cell with fewer than two live neighbors dies, as if caused by under-population.

2. Any live cell with two or three live neighbors lives on to the next generation.

3. Any live cell with more than three live neighbors dies, as if by over-population..

4. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.

Write a function to compute the next state (after one update) of the board given its current state.

Follow up: 

Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.
In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?

解題思路：

另建一個陣列來作，耗費O(M*N)，其程式碼如下：

```java
public class Solution {
    public void gameOfLife(int[][] board) {
        int rows = board.length;
        int cols = board[0].length;
        int[][] newBoard = new int[rows][cols];
        int[] x = {1, -1, 0, 0, 1, -1, 1, -1};
        int[] y = {0, 0, 1, -1, 1, -1, -1, 1};
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                // 計算有附近有多少活人
                int lives = 0;
                for (int k = 0; k < 8; k++) {
                    int newX = i + x[k];
                    int newY = j + y[k];
                    if (newX >= 0 && newX < rows && newY >= 0 && newY < cols) {
                        if (board[newX][newY] == 1) {
                            lives++;
                        }
                    }
                }
                // 根據不同條件來判斷是生是死
                if (board[i][j] == 1) {
                    
                    if (lives < 2 || lives > 3) {
                        newBoard[i][j] = 0;
                    } else {
                        newBoard[i][j] = 1;
                    }
                } else { // if (board[i][j] == 0)
                    if (lives == 3) {
                        newBoard[i][j] = 1;
                    } else {
                        newBoard[i][j] = 0;
                    }
                }
            }
        }
        
        for(int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                board[i][j] = newBoard[i][j];
            }
        } 
    }
}
```


法二：In space 作法：

引由網友的解說：

"由於題目中要求我們用置換方法in-place來解題，所以我們就不能新建一個相同大小的數組，那麼我們只能更新原有數組，但是題目中要求所有的位置必須被同時更新，但是在循環程序中我們還是一個位置一個位置更新的，那麼當一個位置更新了，這個位置成為其他位置的neighbor時，我們怎麼知道其未更新的狀態呢，我們可以使用狀態機轉換：

狀態0： 死細胞轉為死細胞

狀態1： 活細胞轉為活細胞

狀態2： 活細胞轉為死細胞

狀態3： 死細胞轉為活細胞

最後我們對所有狀態對2取餘，那麼狀態0和2就變成死細胞，狀態1和3就是活細胞，達成目的。我們先對原數組進行逐個掃瞄，對於每一個位置，掃瞄其周圍八個位置，如果遇到狀態1或2，就計數器累加1，掃完8個鄰居，如果少於兩個活細胞或者大於三個活細胞，而且當前位置是活細胞的話，標記狀態2，如果正好有三個活細胞且當前是死細胞的話，標記狀態3。完成一遍掃瞄後再對數據掃瞄一遍，對2取餘變成我們想要的結果。"

程式碼如下：

```java
public class Solution {
    public void gameOfLife(int[][] board) {
        int rows = board.length;
        int cols = board[0].length;
        int[][] newBoard = new int[rows][cols];
        int[] x = {1, -1, 0, 0, 1, -1, 1, -1};
        int[] y = {0, 0, 1, -1, 1, -1, -1, 1};
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                // 計算有附近有多少活人
                int lives = 0;
                for (int k = 0; k < 8; k++) {
                    int newX = i + x[k];
                    int newY = j + y[k];
                    if (newX >= 0 && newX < rows && newY >= 0 && newY < cols) {
                        if (board[newX][newY] == 1 || board[newX][newY] == 2) {
                            lives++;
                        }
                    }
                }
                // 根據不同條件來判斷是生是死
                if (board[i][j] == 1) {
                    
                    if (lives < 2 || lives > 3) {
                        board[i][j] = 2;
                    } 
                } else { // if (board[i][j] == 0)
                    if (lives == 3) {
                        board[i][j] = 3;
                    }
                }
            }
        }
        
        for(int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                board[i][j] %= 2;
            }
        } 
    }
}
```
---
###Reference
1. http://www.cnblogs.com/grandyang/p/4854466.html
