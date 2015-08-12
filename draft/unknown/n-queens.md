# N-Queens

> The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.

> Given an integer n, return all distinct solutions to the n-queens puzzle.

> Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space respectively.

```java
ArrayList<ArrayList<String>> solveNQueens(int n) {
    ArrayList<ArrayList<String>> answer = new ArrayList<ArrayList<String>>();
    
    if ( n<=0 ) {
        return answer;
    }
    
    ArrayList<Integer> list = new ArrayList<Integer>();
    ArrayList<Integer> nums = new ArrayList<Integer>();
    for ( int i=0 ; i<n ; i++ ) {
        nums.add(i);
    }
    permuteHelper(answer, list, nums, n);
    
    return answer;
}

public void permuteHelper(ArrayList<ArrayList<String>> answer, ArrayList<Integer> list, ArrayList<Integer> nums, int n) {
    
    if( list.size() == n ) {
        answer.add(drawBoard(new ArrayList<Integer>(list)));
        return;
    }
    
    for ( int i=0 ; i<nums.size() ; i++ ) {
        if( !isValid(list, nums.get(i))) {
            continue;
        }
        
        list.add(nums.get(i));
        nums.remove(i);
        permuteHelper(answer, list, nums, n);
        nums.add(i, list.get(list.size()-1));
        list.remove(list.size()-1);
    } 
}

public Boolean isValid(ArrayList<Integer> cols, int col) {
    
    for( int i=0 ; i<cols.size() ; i++ ) {
        // right-top to left-bottom
        if( cols.get(i)+cols.size()-i == col ) {
            return false;
        }
        // left-top to right-bottom
        if( cols.get(i)-cols.size()+i == col ) {
            return false;   
        }
    }
    return true;
}

public ArrayList<String> drawBoard(ArrayList<Integer> cols) {
    
    ArrayList<String> board = new ArrayList<String>();
    
    for( int i=0 ; i<cols.size() ; i++ ) {
        String row = "";
        for( int k=0 ; k<cols.size() ; k++ ) {
            if ( k == cols.get(i) ) {
                row += "Q";
            } else {
                row += ".";
            }
        }
        board.add(row);
    }
    return board;
}
```