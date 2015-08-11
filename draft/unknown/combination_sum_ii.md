# Combination Sum II

[原題網址](http://www.lintcode.com/en/problem/combination-sum-ii/)

> Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

> Each number in C may only be used once in the combination.

```java
public List<List<Integer>> combinationSum2(int[] num, int target) {
    List<List<Integer>> result = new ArrayList<List<Integer>>();
    if ( num == null || num.length == 0 ) {
        return result;
    }
    boolean[] isOpen = new boolean[num.length];
    Arrays.fill(isOpen, true);
    helper(result, new ArrayList<Integer>(), num, target, target, isOpen);
    return result;
}

public void helper(List<List<Integer>> result, List<Integer> list, int[] num, int target, int remain, boolean[] isOpen) {
    
    if ( remain == 0 ) {
        if ( result.contains(new ArrayList<Integer>(list)) ) {
            return;
        }
        result.add(new ArrayList<Integer>(list));
        return;
    } else if ( remain < 0 ) {
        return;
    }
    
    for ( int i = 0 ; i < num.length ; i++ ) {
        if ( !isOpen[i] || num[i] > remain || ( list.size() > 0 && list.get(list.size()-1) > num[i] )) {
            continue;
        }
        list.add(num[i]);
        isOpen[i] = false;
        helper(result, list, num, target, remain-num[i], isOpen);
        list.remove(list.size()-1);
        isOpen[i] = true;
    }
}
```
