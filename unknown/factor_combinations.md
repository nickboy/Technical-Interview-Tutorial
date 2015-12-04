# Factor Combinations

[]()

題意：


解題思路：

先把所有factor都算出來，再去作combination sum的方式，因為factor可以重複用，所以pos往下傳時不需要加1。

```java
public class Solution {
    List<List<Integer>> res;
    public List<List<Integer>> getFactors(int n) {
        res = new ArrayList<List<Integer>>();
        if (n <= 1) {
            return res;
        }
        List<Integer> factors = new ArrayList<Integer>();
        for (int i = 2; i <= n / 2; i++) {
            if (n % i == 0) {
                factors.add(i);
            }
        }
        
        helper(factors, new ArrayList<Integer>(), n, 1, 0);
        return res;
    }
    
    public void helper(List<Integer> factors, List<Integer> tempRes, int n, int product, int pos) {
        
        if (product == n) {
            res.add(new ArrayList<Integer>(tempRes));
            return;
        }
        
        for (int i = pos; i < factors.size(); i++) {
            if (product * factors.get(i) > n) {
                break;
            }
            tempRes.add(factors.get(i));
            helper(factors, tempRes, n, product * factors.get(i), i);
            tempRes.remove(tempRes.size() - 1);
        }
        
    }
}
```

網友更精簡的解法如下：

```java
public List<List<Integer>> getFactors(int n) {
    List<List<Integer>> result = new ArrayList<List<Integer>>();
    if (n <= 3) return result;
    helper(n, -1, result, new ArrayList<Integer>());
    return result; 
}

public void helper(int n, int lower, List<List<Integer>> result, List<Integer> cur) {
    if (lower != -1) {
        cur.add(n);
        result.add(new ArrayList<Integer>(cur));
        cur.remove(cur.size() - 1);
    }
    int upper = (int) Math.sqrt(n);
    for (int i = Math.max(2, lower); i <= upper; ++i) {
        if (n % i == 0) {
            cur.add(i);
            helper(n / i, i, result, cur);
            cur.remove(cur.size() - 1);
        }
    }
}
```
---
###Reference
1. https://leetcode.com/discuss/58828/a-simple-java-solution