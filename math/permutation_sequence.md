#Permutation Sequence

[Lintcode](http://www.lintcode.com/en/problem/permutation-sequence/)

題意：

Given n and k, return the k-th permutation sequence.

**Example**

For ```n = 3```, all permutations are listed as follows:
```
"123"
"132"
"213"
"231"
"312"
"321"
```
If ```k = 4```, the fourth permutation is ```"231"```

Note
n will be between 1 and 9 inclusive.

**Challenge**

O(n*k) in time complexity is easy, can you do it in O(n^2) or less?

解題思路：

DFS法：用DFS把所有可能全列出來，再返回第k個值，時間複雜度太高，程式碼如下：

```java
class Solution {
    /**
      * @param n: n
      * @param k: the kth permutation
      * @return: return the k-th permutation
      */
      
    List<String> res;
    boolean[] visited;
    public String getPermutation(int n, int k) {
        if (n == 0) {
            return "";
        }
        
        res = new ArrayList<String>();
        visited = new boolean[n];
        helper(n, new StringBuilder());
        return res.get((k - 1));
    }
    
    public void helper(int n, StringBuilder sb) {
        if (sb.length() == n) {
            res.add(sb.toString());
        }
        
        for (int i = 1; i <= n; i++) {
            if (visited[i - 1] == false) {
                sb.append(String.valueOf(i));
                visited[i - 1] = true;
                helper(n, sb);
                sb.deleteCharAt(sb.length() - 1);
                visited[i - 1] = false;
            }
        }
    }
}


```

另有數學解法：


---
###Reference
1. http://blog.hfknight.com/?p=1303
2. https://leetcode.com/discuss/42700/explain-like-im-five-java-solution-in-o-n
