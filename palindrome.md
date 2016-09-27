# Palindrome

```java
public class Palindrome {
    
    
    public int leastEdit(String s) {
        //state:f[i][j] means the least edit needed from s[i~j]
        //init: f[0][0] = 0 f[i][i + 1] = 0 || 1
        //function: add left: f[i][j - 1] + 1, add right: f[i + 1][j] + 1
        //          delete left: f[i + 1][j] + 1     delete right: f[i][j - 1] + 1
        //          change left & right: f[i + 1][j - 1] + 1
        
        int n = s.length();
        
        //state
        int dp[][] = new int[n][n];
        
        //init
        for(int i = 0; i < n - 1; i++) {
            if (s.charAt(i) != s.charAt(i + 1)) {
                dp[i][i + 1] = 1;
            }
        }
        
        //func
        for (int len = 3; len <= n; len++) {
            for (int i = 0; i <= n - len; i++) {
                int j = i + len - 1;
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1];
                } else {
                    dp[i][j] = Math.min(dp[i][j - 1] + 1, dp[i + 1][j] + 1);
                    dp[i][j] = Math.min(dp[i][j], dp[i + 1][j - 1] + 1);
                }
            }
        }
        
        return dp[0][n - 1];
    }
    
    
    public boolean isPali(String s) {
        s = s.toLowerCase();
        
        int left = 0;
        int right = s.length() - 1;
        
        while (left < right) {
            int i = s.charAt(left);
            int j = s.charAt(right);
            
            if (!Character.isLetterOrDigit(i)) {
                left++;
                continue;
            }
            
            if (!Character.isLetterOrDigit(j)) {
                right--;
                continue;
            }
            
            if (i != j) {
                return false;
            }
            
            left++;
            right--;
        }
        
        return true;
    }

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        Palindrome pal = new Palindrome();
        System.out.println(pal.isPali("aba,,"));
        System.out.println(pal.leastEdit("aabac"));

    }

}
```