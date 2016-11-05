# Subset Sum

Given a set of non-negative integers, and a value sum, determine if there is a subset of the given set with sum equal to given sum.

```
Examples: set[] = {3, 34, 4, 12, 5, 2}, sum = 9
Output:  True  //There is a subset (4, 5) with sum 9.
```

Naive Recurrsive Way

时间复杂度指数级别
```java
 static boolean isSubsetSumRecurrsive(int[] set, int sum) {
        if (set == null || set.length == 0) return false;
        
        int n = set.length;
        
        
        return helper(set, n, sum);
    }
    
    static boolean helper(int[] set, int n, int sum) {
        if (sum == 0) return true;
        if (n == 0) return false;
        
        //如果最后一位比sum大， ignore it
        if (set[n - 1] > sum) return helper(set, n - 1, sum);
        
        //ignore last element or substrat the last element 
        return helper(set, n - 1 , sum) || helper(set, n - 1, sum - set[n - 1]);
    }
```

DP: 0(sum*n)

状态方程:

dp[i][j]代表sum为i时，是否能从set[0]~set[j-1]个数中相加得到sum


```
要么不要最后一位，要么减去最后一位看能否得到
if i >= set[j - 1]
dp[i][j] = dp[i][j - 1] || dp[i - set[j-1]][j - 1]
```

```java
    static boolean isSubsetSum(int[] set, int sum) {
        if (set == null || set.length == 0) return false;
        
        int n = set.length;
        boolean[][] dp = new boolean[sum + 1][n + 1]; 
        
        for (int i = 0; i <= n; i++) {
            dp[0][i] = true;
        }
        
        for (int i = 0; i <= sum; i++) {
            dp[i][0] = false;
        }
        
        for (int i = 1; i <= sum; i++) {
            for (int j = 1; j <= n; j++) {
                //先不考虑最后一位的情况
                dp[i][j] = dp[i][j - 1];
                //如果最后一位可以操作，有两种方法，忽略或者减掉最后一位的值
                if (i >= set[j - 1]) {
                    dp[i][j] = dp[i][j] || dp[i - set[j - 1]][j - 1];
                }
            }
        }
        
        return dp[sum][n];
    }
    
    public static void main (String args[])
    {
          int set[] = {3, 34, 4, 12, 5, 2};
          int sum = 9;
          if (isSubsetSumRecurrsive(set, sum) == true)
             System.out.println("Found a subset with given sum");
          else
             System.out.println("No subset with given sum");
    }
```
