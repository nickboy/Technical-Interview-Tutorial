# Sort Transformed Array

##### 題目連結：

[https://leetcode.com/problems/sort-transformed-array/](https://leetcode.com/problems/sort-transformed-array/)

##### 題意：

給定一個有序陣列與A, B, C三值，將陣列中每個元素套入Quadratic function 即$$f(x) = ax^2 + bx + c$$，並將結果以遞增方式表示。

**Example 1:**

```
Input: 
nums = 
[-4,-2,2,4]
, a = 
1
, b = 
3
, c = 
5
Output: 
[3,9,15,33]
```

**Example 2:**

```
Input: 
nums = 
[-4,-2,2,4]
, a = 
-1
, b = 
3
, c = 
5
Output: 
[-23,-5,1,7]
```

解題思路：

###### Option 1:

最簡單的方法即是將每個數算出來並排序，但需耗費$$O(NlogN)$$時間。

###### Option 2: 

數學解法，可惜數學不好沒想到，參考了網上教學後得知以下規則

* 若$$a > 0$$ ，則是個開口向上的曲線，所以絕對值越大的數則得出的數越大，我們可以由後往前寫result陣列。
* 若$$a > 0$$，則是個開口向下的曲線，所以絕對值越大的數則得出來的數越小，我們可以由前往後寫result陣列。
* 若$$a = 0$$，則是個單調遞增的數，往前或往後寫都沒差，可以和上面其中一個case 合併。

程式碼如下：

```java
class Solution {
    public int[] sortTransformedArray(int[] nums, int a, int b, int c) {
        if (nums == null) {
            return nums;
        }
        
        int length = nums.length;
        int[] result = new int[length];
        int left = 0;
        int right = length - 1;
        
        if (a > 0) {
            int cur = length - 1;
            while (left <= right) {
                if (quadraticFunction(nums[left], a, b, c) > quadraticFunction(nums[right], a, b, c)) {
                    result[cur--] = quadraticFunction(nums[left], a, b, c);
                    left++;
                } else {
                    result[cur--] = quadraticFunction(nums[right], a, b, c);
                    right--;
                }
            }
        } else {
            int cur = 0;
            while (left <= right) {
                if (quadraticFunction(nums[left], a, b, c) < quadraticFunction(nums[right], a, b, c)) {
                    result[cur++] = quadraticFunction(nums[left], a, b, c);
                    left++;
                } else {
                    result[cur++] = quadraticFunction(nums[right], a, b, c);
                    right--;
                }
            }
        }
        
        return result;
    }
    
    public int quadraticFunction(int val, int a, int b, int c) {
        int result = a * (val * val) + val * b + c;
        return result;
    }
}
```

##### Reference:

* [https://www.cnblogs.com/grandyang/p/5595614.html](https://www.cnblogs.com/grandyang/p/5595614.html)

* [https://www.mathplanet.com/education/algebra-1/quadratic-equations/the-graph-of-y-ax-2-plus-bx-plus-c](https://www.mathplanet.com/education/algebra-1/quadratic-equations/the-graph-of-y-ax-2-plus-bx-plus-c)



