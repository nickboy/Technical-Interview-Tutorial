#Best Time to Buy and Sell Stock III

[原題網址](http://www.lintcode.com/en/problem/best-time-to-buy-and-sell-stock-iii/)

題意：最多可以作兩次買賣，找出最大獲利值

解題思路：從左掃到右，找出最大獲利值，再從右掃到左，找最大獲利值，接著找出 i ，使得 right[i] + left[i] 為最大。

```java
public int maxProfit(int[] prices) {
    
   if (prices == null || prices.length == 0) {
       return 0;
   }
   
   int len = prices.length;
   int[] left = new int[len];
   int[] right = new int[len];
   
   int profit = 0;
   int min = Integer.MAX_VALUE;
   
   for (int i = 0; i < len; i++) {
       profit = Math.max(profit, prices[i] - min);
       min = Math.min(min, prices[i]);
       left[i] = profit;
   }
   
   profit = 0;
   int max = prices[len - 1];
   for (int i = len - 1; i >= 0; i--) {
       profit = Math.max(profit, max - prices[i]);
       max = Math.max(max, prices[i]);
       right[i] = profit;
   }
   
   int maxProfit = 0;
   for (int i = 0; i < len - 1; i++) {
       maxProfit = Math.max(maxProfit, left[i] + right[i]);
   }
   
   return maxProfit;
}
```

>Time Complexity：$$O(N)$$