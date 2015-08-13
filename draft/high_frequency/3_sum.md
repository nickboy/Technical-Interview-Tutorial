# 3 Sum

[原題網址](http://www.lintcode.com/en/problem/3-sum/)

> Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

```java
public ArrayList<ArrayList<Integer>> threeSum(int[] numbers) {
    // write your code here
    
    ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
    if ( numbers == null || numbers.length < 3 ) {
        return result;
    }
    
    Arrays.sort(numbers);
    
    for ( int i = 0 ; i < numbers.length ; i++ ) {
        if ( i != 0 && numbers[i] == numbers[i-1] ) {
            continue;
        }
        int start = i+1; 
        int end = numbers.length-1;
        int target = -numbers[i];
        while ( start < end ) {
            if ( numbers[start] + numbers[end] == target ) {
                result.add(new ArrayList<Integer>(Arrays.asList(numbers[i], numbers[start], numbers[end])));
                start++;
                end--;
                while ( start < end && numbers[start] == numbers[start-1] ) {
                    start++;
                }
                while ( start < end && numbers[end] == numbers[end+1] ) {
                    end--;
                }
            } else if ( numbers[start] + numbers[end] < target ) {
                start++;
            } else {
                end--;
            }
        }
    }
    return result;
    
}
```

