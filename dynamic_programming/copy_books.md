#Copy Books

[原題網址](http://www.lintcode.com/en/problem/copy-books/)

題意：

Given an array A of integer with size of n( means n books and number of pages of each book) and k people to copy the book. You must distribute the continuous id books to one people to copy. (You can give book A[1],A[2] to one people, but you cannot give book A[1], A[3] to one people, because book A[1] and A[3] is not continuous.) Each person have can copy one page per minute. Return the number of smallest minutes need to copy all the books.

**Example**

Given array ```A = [3,2,4], k = 2.```

Return ```5```( First person spends 5 minutes to copy book 1 and book 2 and second person spends 4 minutes to copy book 3. )

**Challenge**

Could you do this in O(n*k) time ?

解題思路：利用動態規劃來幫助我們解這道題，狀態轉換如下：

>mins[i][j] ：代表前i個人抄第j本書的最少時間為多少。

>$$mins[i][j] = min( max( mins[i-1][t], sum(t+1, j) ), where 1 <= i <= k, 0 <= j <= n - 1, 0 <= t < j$$

>


```java
public int copyBooks(int[] pages, int k) {
    
    int len = pages.length;
    k = Math.min(k, len); //若k多於書本書，多出來的那些人不需要
    
    int[] sumFromStart = new int[len];
    int sum = 0;
    for (int i = 0; i < len; i++) {
        sum += pages[i];
        sumFromStart[i] = sum;
    }
    
    // mins[i][j] ：代表前i個人抄第j本書的最少時間為多少。
    int[][] mins = new int[k + 1][len];
    for (int i = 0; i <= k; i++) {
        for (int j = 0; j < len; j++) {
            mins[i][j] = Integer.MAX_VALUE;
        }
    }
    
    for (int i = 1; i <= k; i++) {
        for (int j = 0; j < len; j++) {
            if (i == 1 || j == 0) { 
                // 如果只有一位writer，則讓他抄前j本書，
                // 如果只有一本書，則讓一位writer抄那本書
                mins[i][j] = sumFromStart[j];
            } else {
                for (int t = j - 1; t >= 0; t--) {
                    // 在此枚舉從j-1到0本的最小抄書時間，
                    // 代表前i-1個人抄前t本書，最後那個人抄從j+1到t本書，
                    // 取max是因為若其中一群人抄完了，而另一個人還沒抄完，則等他的時間也要算進去
                    // 反之亦然
                    int cur = Math.max(mins[i-1][t], sumFromStart[j] - sumFromStart[t]);
                    mins[i][j] = Math.min(cur, mins[i][j]);
                }
            }
        }
    }
    
    return mins[k][len - 1];
}
```

---
###Reference
1. http://sidbai.github.io/2015/07/25/Copy-Books/