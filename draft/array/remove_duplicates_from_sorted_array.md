# Remove Duplicates from Sorted Array I
[原題網址](http://www.lintcode.com/en/problem/remove-duplicates-from-sorted-array/)

```java
public int removeDuplicates(int[] nums) {
    // write your code here
    if (nums.length == 0 || nums == null) {
        return 0;
    }
    //use two pointer approach
    //first pointer point to last non duplicate element
    //second pointer travse whole list.
    int pos = 0;
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] != nums[pos]) {
            pos += 1;
            nums[pos] = nums[i];
        }
    }
    // since index is start from 0
    return pos + 1;
}
```


# Remove Duplicates from Sorted Array II

[原題網址](http://www.lintcode.com/en/problem/remove-duplicates-from-sorted-array-ii/)
>Follow up for "Remove Duplicates":

>What if duplicates are allowed at most twice?

```java
public int removeDuplicates(int[] nums) {
    int len = nums.length;
    if (len <= 2) {
        return len;
    }
    int pre = 1;
    int cur = 1;
    int occur = 1;
    while (cur < len) {
        if (nums[cur] == nums[cur - 1]) {
            if (occur >= 2) {
                //超過規定數目，直接忽略目前值，往下一個前進
                //設continue 就是只往前，而不作assign的動作，且也防止out of bound問題
                cur++;
                continue;
            } else {
                //還沒超過規定數目，因此occur++
                occur++;
            }
        } else {
            //因不同，而重新計算，occur重設
            occur = 1;
        }
        //每輪不管如何，都把cur的值assign給pre
        nums[pre] = nums[cur];
        pre++;
        cur++;
    }
    return pre;
}
```
