#Longest Increasing Subsequence
[原題網址](http://www.lintcode.com/en/problem/longest-increasing-subsequence/)

```java
public int longestIncreasingSubsequence(int[] nums) {
    
    int[] result = new int[nums.length];
    int max = 0;
    
    for (int i = 0; i < nums.length; i++) {
        result[i] = 1;
        
        for (int j = 0; j < i; j++) {
            //拿之前的與目前這個比，若比較小，則看看result誰大就取誰
            if (nums[j] <= nums[i]) {
                result[i] = result[i] > result[j] + 1 ? result[i] : result[j] + 1;
            }
        }
        
        if (max < result[i]) {
            max = result[i];
        }
    }

    return max;
    
}
```