# House Robber
```
House Robber

You are a professional robber planning to rob houses along a street.

Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

```

DP[i] = max(dp[i - 1], dp[i - 2] + num[i])
* 要么是不要当前这家，要么不要前一家

```java
public class Solution {
    public int rob(int[] nums) {
        //dp[i] = Math.max(dp[i - 2] + num[i - 1], dp[i - 1])
        if (nums == null || nums.length == 0) return 0;
        
        
        int[] dp = new int[nums.length + 1];
        
        dp[0] = 0;
        dp[1] = nums[0];
        
        for (int i = 2; i <= nums.length; i++) {
            dp[i] = Math.max(dp[i - 2] + nums[i - 1], dp[i - 1]);
        }
        
        return dp[nums.length];
    }
}
```

Follow Up: House Robber II

如果所有人家都在一个环上，最后一家和第一家相连，问最大值

两个dp
* dp代表从第一个房子开始搜刮，不能搜最后一房
* dp2代表从第二个房子开始搜刮，可以搜最后一房
* 最后比一下 谁大取谁

```java
public class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        
        //这句一定要加！！
        if (nums.length == 1) return nums[0];
        int n = nums.length;
        int[] dp = new int[n + 1];
        int[] dp2 = new int[n + 1];
        //dp代表从第一个房子开始搜刮，不能搜最后一房
        //dp2代表从第二个房子开始搜刮，可以搜最后一房
        dp[0] = 0;
        dp[1] = nums[0];
        dp2[0] = 0;
        dp2[1] = 0;
        for (int i = 2; i <= n; i++) {
            dp[i] = Math.max(dp[i - 2] + nums[i - 1], dp[i - 1]);
            dp2[i] = Math.max(dp2[i - 2] + nums[i - 1], dp2[i - 1]);
        }
        
        int startFromFirst = dp[nums.length - 1];
        
        
        int startFromSecond = dp2[nums.length];
        
        return Math.max(startFromFirst, startFromSecond);
    }
}
```


