# Longest Common Subsequence

二刷
* 如果最后一位俩字符不相等，那么他就不可能同时出现在subsequence当中，根据这一特性缩小范围。


注意判断最后一个字符是否相等


```java
public int longestCommonSubsequence(String A, String B) {
        int n = A.length();
        int m = B.length();
        
        int f[][] = new int [n + 1][m + 1];
        
        for (int i = 0; i < n + 1; i++) {
            f[i][0] = 0;
        }
        
        for (int j = 0; j < m + 1; j++) {
            f[0][j] = 0;
        }
        
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                
                if (A.charAt(i - 1) == B.charAt(j - 1)) {
                    f[i][j] = f[i - 1][j - 1] + 1;                    
                } else {
                    f[i][j] = Math.max(f[i - 1][j], f[i][j - 1]);
                }
            }
        }
        
        return f[n][m];
    }
```

Related

Edit distance

https://leetcode.com/problems/edit-distance/

f[i][j] a的前i个字符最少编辑几次变成b的前j个字符

```java
    public int minDistance(String word1, String word2) {
        //state
        int m = word1.length();
        int n = word2.length();
        
        int[][] dp = new int[m + 1][n + 1];
        
        //init
        for (int i = 0; i < m + 1; i++) {
            dp[i][0] = i;
        }
        
        for (int j = 0; j < n + 1; j++) {
            dp[0][j] = j;
        }
        
        //function
        for (int i = 1; i < m + 1; i++) {
            for (int j = 1; j < n + 1; j++) {
                //注意这里 charAt(i - 1)
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = Math.min(dp[i - 1][j] + 1, dp[i][j - 1] + 1);
                    dp[i][j] = Math.min(dp[i][j], dp[i - 1][j - 1]);
                } else {
                    dp[i][j] = Math.min(dp[i - 1][j] + 1, dp[i][j - 1] + 1);
                    dp[i][j] = Math.min(dp[i][j], dp[i - 1][j - 1] + 1);
                }
                
            }
        }
        
        return dp[m][n];
    }
```

 Distinct Subsequences

http://www.lintcode.com/en/problem/distinct-subsequences/

