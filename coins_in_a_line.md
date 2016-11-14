# Coins In a Line

```
一串数，两个玩家，每次轮流选一个数并且只能选最左或最右，
在你先选并且对手很聪明的情况下，怎样max你的和。

Example:
{5, 3, 7, 10}，应该返回15
{8, 15, 3, 7}，应该返回22

```

经典区间动归
* dp[i][j] 代表从i到j这个区间取到的最大金币
* 初始化：
  * i和j一样时候就取coins[i]
  * i和j相邻去max(coins[i], coins[j])
* 方程：
  * 比较取左取右哪个大，取左的话，再加上等待对手取完多的金币的那一部分，取右同理（因为假设对手很聪明，他肯定会取剩下的里多的金币，那你只能取剩下的那块区间）
  * ```dp[i][j] = max(coins[i] + min(dp[i+1][j-1],dp[i+2][j]), coins[j]+ min(dp[i+1][j-1],dp[i][j-2]))```


```java
public class CoinsInALine {
    public static int maxCoins(int[] a) {
        if (a == null || a.length == 0) return 0;
        if (a.length == 1) return a[0];
        
        int[][] dp = new int[a.length][a.length];
        
        for (int i = 0; i < a.length; i++) {
            dp[i][i] = a[i];
        }
        
        for (int i = 0; i < a.length - 1; i++) {
            dp[i][i + 1] = Math.max(a[i], a[i + 1]);
        }
        
        for (int len = 2; len <= a.length; len++) {
            for (int start = 0; start + len < a.length; start++) {
                int end = start + len;
                dp[start][end] = Math.max(a[start] + Math.min(dp[start + 1][end - 1], dp[start + 2][end]), 
                        a[end] + Math.min(dp[start][end - 2], dp[start + 1][end - 1]));
            }
        }
        
        return dp[0][a.length - 1];
    }
    

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        int[] a = {5,3,7,10};
        int[] b = {8,15,3,7};
        System.out.println(maxCoins(a));
        System.out.println(maxCoins(b));

    }

}
```