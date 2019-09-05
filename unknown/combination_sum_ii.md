# Combination Sum II

[原題網址](http://www.lintcode.com/en/problem/combination-sum-ii/)

> Given a collection of candidate numbers \(C\) and a target number \(T\), find all unique combinations in C where the candidate numbers sums to T.
>
> Each number in C may only be used once in the combination.

updated on 2019.9.4

```java
class Solution {
    
    List<List<Integer>> globalResult;
    
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        globalResult = new ArrayList<>();
        Arrays.sort(candidates);
        if (candidates == null || candidates.length == 0 || target == 0) {
            return globalResult;
        }
        
        helper(candidates, target, new ArrayList<>(), 0);
        return globalResult;
    }
    
    public void helper(int[] candidates, int target, List<Integer> tempRes, int pos) {
        if (target == 0) {
            globalResult.add(new ArrayList(tempRes));
            return;
        }
        if (target < 0) {
            return;
        }
        
        for (int i = pos; i < candidates.length; i++) {
            // Check if we use duplicate candidate, skip it if we used same value before.
            if (i > pos && candidates[i] == candidates[i - 1]) {
                continue;
            }
            
            // Prune the path as we don't need to dive deeper and save time.
            if (target < candidates[i]) {
                break;
            }
            tempRes.add(candidates[i]);
            helper(candidates, target - candidates[i], tempRes, i + 1);
            tempRes.remove(tempRes.size() - 1);
        }
    }
}
```



