# Maximum Subarray

http://www.lintcode.com/en/problem/maximum-subarray/

解法一

Kadane's Algorithm

https://en.wikipedia.org/wiki/Maximum_subarray_problem

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
    int max = Integer.MIN_VALUE, sum = 0;
    for (int i = 0; i < A.length; i++) {
        if (sum < 0) 
            sum = A[i];
        else 
            sum += A[i];
        if (sum > max)
            max = sum;
    }
    return max;
}
```


Related Problem

Best Time to Buy and Sell Stock
 
http://www.lintcode.com/en/problem/best-time-to-buy-and-sell-stock/#

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

```java
    public int maxProfit(int[] prices) {
        // 这种方法是for 其中一个数， 然后让另外的变量最优
        if (prices == null || prices.length == 0) {
            return 0;
        }

        int min = Integer.MAX_VALUE;  //just remember the smallest price
        int profit = 0;
        for (int i : prices) {
            if (i < min) {
                min = i;
            }
            
            if ((i - min) > profit) {
                profit = i - min;
            }
        }

        return profit;
    }
```
 
 Maximum Subarray II

http://www.lintcode.com/en/problem/maximum-subarray-ii/

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

取相反数 算Maximum SubArray, 最后再反一下