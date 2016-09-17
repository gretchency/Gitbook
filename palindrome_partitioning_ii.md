# Palindrome Partitioning II

http://www.lintcode.com/en/problem/palindrome-partitioning-ii/#

Given s = "aab",

Return 1 since the palindrome partitioning ["aa", "b"] could be produced using 1 cut.

把一个字符串分成j, j + 1 ~ i，

保证j + 1 ~ i是回文，求f(j)的最小分割数，最后加上最后一刀1


```java
//区间 + 序列动归
    
    public boolean[][] getIsPalindrome(String s) {
        boolean[][] res = new boolean[s.length()][s.length()];
        
        for (int i = 0; i < s.length(); i++) {
            res[i][i] = true;
        }
        
        for (int i = 0; i < s.length() - 1; i++) {
            res[i][i + 1] = (s.charAt(i) == s.charAt(i + 1));
        }
        
        //最少三个字符
        //区间动归先for 区间长度
        for (int len = 2; len <= s.length(); len++) {
            for (int start = 0; start + len < s.length(); start++) {
                res[start][start + len] = (s.charAt(start) == s.charAt(start + len) && res[start + 1][start + len - 1]);
            }
        }
        
        return res;
    }
    
    public int minCut(String s) {
        if (s == null || s.length() == 0) return -1;
        
        int n = s.length();
        
        //prep
        boolean[][] isPal = getIsPalindrome(s);
        
        //state
        int[] dp = new int[n + 1];
        
        //init
        for (int i = 0; i < n + 1; i++) {
            dp[i] = i - 1;
        }
        
        //function
        for (int i = 1; i < n + 1; i++) {
            for (int j = 0; j < i; j++) {
                if(isPal[j][i - 1]) {
                    dp[i] = Math.min(dp[i], dp[j] + 1);
                }
            }
        }
        
        
        //Answer
        return dp[n];
    }
```