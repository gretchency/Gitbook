# Longest Common Subsequence

```java
public class Solution {
    /**
     * @param A, B: Two strings.
     * @return: The length of longest common subsequence of A and B.
     */
    public int longestCommonSubsequence(String A, String B) {
        // 为啥没有初始化f[0][j], f[i][0]也过了
        int n = A.length();
        int m = B.length();
        
        int f[][] = new int [n + 1][m + 1];
        
        
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                f[0][j] = 0;
                f[i][0] = 0;
                f[i][j] = Math.max(f[i - 1][j], f[i][j - 1]);
                
                
                if (A.charAt(i - 1) == B.charAt(j - 1)) {
                    f[i][j] = f[i - 1][j - 1] + 1;                    
                }
            }
        }
        
        return f[n][m];
    }
}
```