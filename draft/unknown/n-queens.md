# N-Queens

> The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.

> Given an integer n, return all distinct solutions to the n-queens puzzle.

> Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space respectively.

```java
public ArrayList<ArrayList<String>> solveNQueens(int n) {
    ArrayList<ArrayList<String>> result = new ArrayList<ArrayList<String>>();
    if ( n < 1 ) {
        return result;
    }
    helper(result, new ArrayList<Integer>(), n);
    return result;
}

public void helper(ArrayList<ArrayList<String>> result, ArrayList<Integer> list, int n) {
    if ( list.size() == n ) {
        // result.add(new ArrayList<Integer>(list));
        result.add(draw(list));
        return;
    }
    
    for ( int i = 0 ; i < n ; i++ ) {
        if ( !isValid(list, i) ) {
            continue;
        }
        list.add(i);
        helper(result, list, n);
        list.remove(list.size()-1);
    }
}

public boolean isValid(ArrayList<Integer> list, int n) {
    for ( int i = 0 ; i < list.size() ; i++ ) {
        if ( list.get(i).equals(n) ) {
            return false;
        }
        if ( list.size() + n == i + list.get(i) ) {
            return false;
        }
        if ( list.size() - n == i - list.get(i) ) {
            return false;
        }
    }
    return true;
}

public ArrayList<String> draw(ArrayList<Integer> list) {
    ArrayList<String> board = new ArrayList<String>();
    for ( int i = 0 ; i < list.size() ; i++ ) {
        char[] row = new char[list.size()];
        Arrays.fill(row, '.');
        row[list.get(i)] = 'Q';
        board.add(new String(row));
    }
    return board;
}
```