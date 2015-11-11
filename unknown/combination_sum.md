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


非遞迴寫法

```java
public List<List<Integer>> combinationSum(int[] candidates, int target) {
    Arrays.sort(candidates);
    List<List<List<Integer>>> dp = new ArrayList<List<List<Integer>>>();
    for (int i = 1; i <= target; i++) {
        List<List<Integer>> list_i = new ArrayList<List<Integer>>();
        for (int j = 0; j < candidates.length && candidates[j] <= i; j++) {
            if (i == candidates[j]).
                list_i.add(Arrays.asList(candidates[j]));
            else {
                for (List<Integer> l : dp.get(i - 1 - candidates[j])) {
                    if (candidates[j] <= l.get(0)) {
                        List<Integer> tmp = new ArrayList<Integer>();
                        tmp.add(candidates[j]);
                        tmp.addAll(l);
                        if (!list_i.contains(tmp)). From 1point 3acres bbs
                            list_i.add(tmp);. 1point3acres.com/bbs
                    }
                }
            }
        }
.       dp.add(list_i);
    }
    return dp.get(target - 1);
}
```


11.9.2015 updated

```java
public class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (candidates == null || candidates.length == 0) {
            return res;
        }
        Arrays.sort(candidates);
        helper(candidates, target, new ArrayList<Integer>(), res, 0);
        return res;
    }
    
    private void helper(int[] candidates, int target, List<Integer> tempRes, List<List<Integer>> res, int pos) {
        if (target == 0) {
            res.add(new ArrayList<Integer>(tempRes));
            return;
        }
        
        //用prev來判斷是否有重複的
        int prev = -1;
        
        for (int i = pos; i < candidates.length; i++) {
            
            // 一旦比target大，後面也不用比了
            if (candidates[i] > target) {
                break;
            }
            
            if (prev != -1 && prev == candidates[i]) {
                continue;
            }
            
            tempRes.add(candidates[i]);
            helper(candidates, target - candidates[i], tempRes, res, i);
            tempRes.remove(tempRes.size() - 1);
            prev = candidates[i];
        }
    }
}
```

進階 [Combination Sum II](combination_sum_ii.md)
