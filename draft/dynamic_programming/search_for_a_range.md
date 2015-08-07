#Search for a Range
[原題網址](http://www.lintcode.com/en/problem/search-for-a-range/)

>解法：跑兩次二分搜尋，第一次找目標值的第一個發生的位置，第二次找目標值最後發生的位置。

```java
public ArrayList<Integer> searchRange(ArrayList<Integer> A, int target) {
        
    int start;
    int end;
    int mid; 
    int midValue;
    int[] range = {-1, -1};
    
    if (A.size() == 0) {
        //you can not direct pass array as paramemter to constructor
        return new ArrayList<Integer>(Arrays.asList(range[0], range[1]));
    }
    
    
    //search lower bound
    start = 0;
    end = A.size() - 1;
    while (start + 1 < end) {
        mid = start + (end - start) / 2;
        midValue = A.get(mid);
        if (midValue == target) {
            //move end ahead since you need to find the first occur element
            end = mid;
        } else if (midValue < target) {
            start = mid;
        } else if (midValue > target) {
            end = mid;
        }
    }
    //since you need to find first occur element, detect start first.
    if (A.get(start) == target) {
        range[0] = start;
    } else if (A.get(end) == target) {
        range[0] = end;
    } else {
        //return directly, since you can not find anything
        range[0] = range[1] = -1;
        return new ArrayList<Integer>(Arrays.asList(range[0], range[1]));
    }
    
    //search upper bound
    start = 0;
    end = A.size() - 1;
    
    while (start + 1 < end) {
        mid = start + (end - start) / 2;
        midValue = A.get(mid);
        if (midValue == target) {
            // move start backward since you need to find the last occur element
            start = mid;
        } else if (midValue < target) {
            start = mid;
        } else {
            end = mid;
        }
    }
    // detect end first, since you need to find the last occur element.
    if (A.get(end) == target) {
        range[1] = end;
    } else if (A.get(start) == target) {
        range[1] = start;
    } else {
        range[1] = range[0] = -1;
        return new ArrayList<Integer>(Arrays.asList(range[0], range[1]));
    }
    
    return new ArrayList<Integer>(Arrays.asList(range[0], range[1]));
}
```

>Time Complexity：O(NlogN)