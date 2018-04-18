# Maximum Subarray

[http://www.lintcode.com/en/problem/maximum-subarray/](http://www.lintcode.com/en/problem/maximum-subarray/)  


[https://www.youtube.com/watch?v=epTQfFlhQBo](https://www.youtube.com/watch?v=epTQfFlhQBo)

解法一

Kadane's Algorithm  
[https://en.wikipedia.org/wiki/Maximum\_subarray\_problem](https://en.wikipedia.org/wiki/Maximum_subarray_problem)

* maxCur 表示以nums\[i\]结尾的子序列的最大和

* 如果之前数组和为负，则自立门户，自己就是目前为止最高的maxSubarray中的值
* 如果之前数组和为正，则热烈投入其怀抱，加入其中
* 即 dp\[i\] = dp\[i-1\]&gt;0? dp\[i-1\]+nums\[i\] : nums\[i\]

```java
public int maxSubArray(int[] nums) {
        
        int maxCur = nums[0];
        int maxAll = nums[0];

        //一定注意从1开始循环！！！
        for (int i = 1; i < nums.length; i++) {
            maxCur = Math.max(maxCur + nums[i], nums[i]);
            maxAll = Math.max(maxCur, maxAll);
        }

        return maxAll;
    }
```

解法二：

通俗易懂

```java
public class Solution {
public int maxSubArray(int[] A) {
       if (nums == null || nums.length == 0) return -1;

       int sum = 0;
       int res = Integer.MIN_VALUE;

       for (int i = 0; i < nums.length; i++) {
           sum += nums[i];
           //记录当前最大
           res = Math.max(sum, res); 
           //如果sum < 0 就割肉，如果大于0，即使变小也保留着看下次是否变大
           if (sum < 0) {
               sum = 0;
           }

       }

       return res;
}
```

Related Problem

Best Time to Buy and Sell Stock

[http://www.lintcode.com/en/problem/best-time-to-buy-and-sell-stock/\#](http://www.lintcode.com/en/problem/best-time-to-buy-and-sell-stock/#)

```
3 ， 2， 3， 1， 2
  -1   1   -2  1
```

要求第一行的最大盈利，实际上就是求第二行的Maximum SubArray

解法一：

```java
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }

        int maxCur = 0;
        int maxAll = 0;

        for (int i = 1; i < prices.length; i++) {
            maxCur = Math.max(0, maxCur + (prices[i] - prices[i - 1]));
            maxAll = Math.max(maxCur, maxAll);
        }

        return maxAll;
    }
```

解法二：  
记录波谷，更新最大差值

```java
    public int maxProfit(int[] prices) {
        // 这种方法是for 其中一个数， 然后让另外的变量最优
        if (prices == null || prices.length == 0) {
            return 0;
        }

        int min = Integer.MAX_VALUE;  //just remember the smallest price
        int profit = 0;

        for(int price: prices) {
          min = Math.min(min, price);
          profit = Math.max(profit, price - min);
        }

        return profit;
    }
```

Maximum Subarray II

[http://www.lintcode.com/en/problem/maximum-subarray-ii/](http://www.lintcode.com/en/problem/maximum-subarray-ii/)

```java
    public int maxTwoSubArrays(ArrayList<Integer> nums) {
        // 中间切一刀，找出左边最大的和右边最大的

        int size = nums.size();

        int left[] = new int[size];
        int right[] = new int[size];

        int maxCur = nums.get(0); 
        int maxAll = nums.get(0);

        left[0] = maxAll;

        for (int i = 1; i < size; i++) {
            maxCur = Math.max(nums.get(i), maxCur + nums.get(i));
            maxAll = Math.max(maxAll, maxCur);

            left[i] = maxAll;
        }


        //右侧从右往左走
        maxCur = nums.get(size - 1);
        maxAll = nums.get(size - 1);

        right[size - 1] = maxAll;

        for (int i = size - 2; i >= 0; i--) {
            maxCur = Math.max(nums.get(i), maxCur + nums.get(i));
            maxAll = Math.max(maxAll, maxCur);

            right[i] = maxAll;
        }

        maxAll = Integer.MIN_VALUE;

        for (int i = 0; i < size - 1; i++) {
            maxAll = Math.max(maxAll, left[i] + right[i + 1]);
        }

        return maxAll;

    }
```

Minimum Subarray

[http://www.lintcode.com/en/problem/minimum-subarray/](http://www.lintcode.com/en/problem/minimum-subarray/)

取相反数 算Maximum SubArray, 最后再反一下

Maximum Subarray Difference

左右分割 分别求出左边的最小和最大subArray 右边最小最大subArray 然后去最大difference

