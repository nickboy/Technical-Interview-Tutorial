#Number of Islands

[]()

題意：0代表海洋，1代表陸地，找出連通陸地的個數

解題思路：可以將陣列轉為無向圖，接著再透過之前找連通圖的方式來作，但轉換圖有點麻煩。我們可以利用一個改良型的深度搜索，每經過一點，便把該點改為海洋，每一次 traverse 則代表一塊陸地。

可先設好一個方向陣列，不斷的去查詢該點的上下左右，並注意座標不會超過矩陣的範圍。

程式如下

```java
public class Solution {
    /**
     * @param grid a boolean 2D matrix
     * @return an integer
     */
     
    public int numIslands(boolean[][] grid) {
        
        if (grid == null || grid.length == 0) {
            return 0;
        }
        
        int m = grid.length;
        int n = grid[0].length;
        int count = 0;
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == true) {
                    count++;
                    dfsMark(grid, i, j, m, n);
                }
            }
        }
        
        return count;
        
    }
    
    private void dfsMark(boolean[][] grid, int row, int col, int rows, int cols) {
        // 方向矩陣，用來幫助我們探測當前節點的上下左右節點
        int[][] directions = new int[][] { {-1, 0}, {1, 0}, {0, -1}, {0, 1} };
        // 因該點已走過，直接設為false以防下次再經過
        grid[row][col] = false;
        
        for (int i = 0; i < directions.length; i++) {
            int newRow = row + directions[i][0];
            int newCol = col + directions[i][1];
            // 注意點沒超過邊際條件
            if (newRow >= 0 && newRow < rows && newCol >= 0 && newCol < cols) {
                if (grid[newRow][newCol] == true) {
                    dfsMark(grid, newRow, newCol, rows, cols);
                } 
            }
        }
    }
}

```

>Time Complexity：O($$N^{2}$$)