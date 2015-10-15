# Remove Element

[Lintcode](http://www.lintcode.com/en/problem/remove-element/)

題意：


解題思路：

使用兩根指針 i 與 j ，j負責走訪整個陣列，i負責指向最後一個不重複的元素，程式碼如下：

```java
public class Solution {
    /** 
     *@param A: A list of integers
     *@param elem: An integer
     *@return: The new length after remove
     */
    public int removeElement(int[] A, int elem) {
        int i = 0;
        int j = 0;
        while (j < A.length) {
            if (A[j] == elem) {
                j++;
            } else {
                A[i] = A[j];
                j++;
                i++;
            }
        }
        return i;
    }
}


```