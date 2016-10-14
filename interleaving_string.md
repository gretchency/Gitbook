# Interleaving String
S1 S2 能否凑成 S3
状态：s1的前i个字符和s2的前j个字符能否凑成s3的前i+j个字符

* 状态方程dp[i][j]满足两种条件：
* 由于S3的每一位都由s1或s2中相应位置字符构成

1. dp[i - 1][j] 然后s1和s3相应位置最后一位相等
2. dp[i][j - 1] 然后s2和s3相应位置最后一位相等

```java
{
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s1 == null || s2 == null || s3 == null) return false;
        
        int m = s1.length();
        int n = s2.length();
        int k = s3.length();
        if (m + n != k) return false;
        
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        
        for (int i = 1; i <= m; i++) {
            //初始化时要注意判断之前是否也相等
            if (s1.charAt(i - 1) == s3.charAt(i - 1) && dp[i - 1][0]) {
                dp[i][0] = true;
            }
        }
        
        for (int i = 1; i <= n; i++) {
            if (s2.charAt(i - 1) == s3.charAt(i - 1) && dp[0][i - 1]) {
                dp[0][i] = true;
            }
        }
        
        //dp[i][j] = dp[i - 1][j] && s1[i - 1] == s3[i + j - 1] || dp[i][j - 1] && s2[j - 1] == s3[i + j -1]
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                dp[i][j] = ((dp[i - 1][j] && s1.charAt(i - 1) == s3.charAt(i + j - 1)) || (dp[i][j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1)));
            }
        }
        
        return dp[m][n];
    }
}
```