# Combinations

[原題網址](http://www.lintcode.com/en/problem/combinations/)

> Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

利用基本的DFS遞迴模板去做

```java
public List<List<Integer>> combine(int n, int k) {
	List<List<Integer>> result = new ArrayList<List<Integer>>();
	if ( n < 1 || k < 1 ) {
	    return result;
	}
	
	helper(result, new ArrayList<Integer>(), n, k, 1);
	
	return result;
}

public void helper(List<List<Integer>> result, List<Integer> list, int n, int k, int pos) {
    
    if ( k == 0 ) {
        result.add(new ArrayList<Integer>(list));
        return;
    }
    
    for ( int i = pos ; i <= n ; i++ ) {
        list.add(i);
        helper(result, list, n, k-1, i+1);
        list.remove(list.size()-1);
    }
}
```