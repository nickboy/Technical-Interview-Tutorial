# Combination Sum

[原題網址](http://www.lintcode.com/en/problem/combination-sum/)

> Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

> The same repeated number may be chosen from C unlimited number of times.

> For example, given candidate set 2,3,6,7 and target 7, 

> A solution set is: 
> `[7]` `[2, 2, 3]`

```java
public List<List<Integer>> combinationSum(int[] candidates, int target) {
    List<List<Integer>> result = new ArrayList<List<Integer>>();
    
    helper(result, new ArrayList<Integer>(), candidates, target);
    
    return result;
}

public void helper(List<List<Integer>> result, List<Integer> list, int[] candidates, int target) {
    
    if( sum(list) == target ) {
        result.add(new ArrayList<Integer>(list));
        return;
    } else if ( sum(list) > target ) {
        return;
    }
    
    for ( int i=0 ; i<candidates.length ; i++ ) {
        if( list.size()>0 && candidates[i] < list.get(list.size()-1) ) {
            continue;
        }
        list.add(candidates[i]);
        helper(result, list, candidates, target);
        list.remove(list.size()-1);
    }
}

public int sum(List<Integer> list) {
    int sum = 0;
    for ( int i=0 ; i<list.size() ; i++ ) {
        sum += list.get(i);
    }
    return sum;
}
```

進階 [Combination Sum II](combination_sum_ii.md)
