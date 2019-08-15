# Pascal Triangle

[Leetcode](https://leetcode.com/problems/pascals-triangle/)

題意：

Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,  
Return

```
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

解題思路：

保持一個pre list，每次在pre list的第一個位置加1，再接著修改中間的值，最後加回result list。

```java
public class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (numRows == 0) {
            return res;
        }
        List<Integer> pre = new ArrayList<Integer>();
        pre.add(1);
        res.add(pre);
        for (int i = 2; i <= numRows; i++) {
            List<Integer> cur = new ArrayList<Integer>();
            cur.add(1);
            for(int j = 0; j < pre.size() - 1; j++) {
                cur.add(pre.get(j) + pre.get(j + 1));
            }
            cur.add(1);
            pre = cur;
            res.add(cur);
        }

        return res;
    }
}
```

More elegant solution \[Updated on 2019.8.13\]

```java
public class Solution {
    public List<List<Integer>> generate(int numRows)
    {
        List<List<Integer>> allrows = new ArrayList<List<Integer>>();
        ArrayList<Integer> row = new ArrayList<Integer>();
        for(int i=0;i<numRows;i++)
        {
            row.add(0, 1);
            for(int j = 1; j < row.size() - 1; j++)
                row.set(j, row.get(j) + row.get(j + 1));
            allrows.add(new ArrayList<Integer>(row));
        }
        return allrows;
    }

}
```

---

### Reference

1. [http://blog.csdn.net/linhuanmars/article/details/23311527](http://blog.csdn.net/linhuanmars/article/details/23311527)
2. [https://leetcode.com/problems/pascals-triangle/discuss/38141/My-concise-solution-in-Java](https://leetcode.com/problems/pascals-triangle/discuss/38141/My-concise-solution-in-Java)



