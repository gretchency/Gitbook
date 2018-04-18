# Best Time To Buy And Sell Stock

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)

两个dp 左边从左往右dp 右边从右往左dp 最后加起来比较得到最大值

```java
public class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) return 0;

        int[] left = new int[prices.length + 1];

        left[1] = 0;  
        int min = prices[0];
        for (int i = 2; i <= prices.length; i++) {
            //逢低买 逢高卖 从左往右时候记录波谷

            min = Math.min(min, prices[i - 1]);
            left[i] = Math.max(left[i - 1], prices[i - 1] - min);
        }

        int[] right = new int[prices.length + 1];

        right[prices.length] = 0;
        int max = prices[prices.length - 1];
        for (int i = prices.length - 1; i >= 1; i--) {
            //逢低买 逢高卖 从右往左时候记录波峰，因为右边是卖，所以要找最大的！

            max = Math.max(max, prices[i - 1]);
            right[i] = Math.max(right[i + 1], max - prices[i - 1]);
        }

        int sum = 0;
        for (int i = 1; i <= prices.length; i++) {
            sum = Math.max(sum, left[i] + right[i]);
        }
        return sum;
    }


}
```

```java
public class Solution {
    /**
     * @param prices: Given an integer array
     * @return: Maximum profit
     */
    public int maxProfit(int[] prices) {
        // write your code here
        if (prices == null || prices.length < 2) return 0;
        
        int[] left = new int[prices.length];
        
        left[0] = 0;
        int min = prices[0];
        
        for (int i = 1; i < prices.length; i++) {
           //逢低买 逢高卖 从左往右时候记录波谷
            min = Math.min(min, prices[i]);
            left[i] = Math.max(left[i - 1], prices[i] - min);
        }
        
        int[] right = new int[prices.length];
        
        right[prices.length - 1] = 0;
        int max = prices[prices.length - 1];
        
        for (int i = prices.length - 2; i >= 1; i--) {
           //逢低买 逢高卖 从右往左时候记录波峰，因为右边是卖，所以要找最大的！
            max = Math.max(max, prices[i]);
            right[i] = Math.max(right[i + 1], max - prices[i]);
        }
        
        int sum = 0;
        for (int i = 0; i < prices.length; i++) {
            sum = Math.max(sum, left[i] + right[i]);
        }
        
        return sum;
    }
}
```



