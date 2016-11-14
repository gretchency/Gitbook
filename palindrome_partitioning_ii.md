# Palindrome Partitioning II

http://www.lintcode.com/en/problem/palindrome-partitioning-ii/#

```
Given s = "aab",

Return 1 since the palindrome partitioning ["aa", "b"] could be produced using 1 cut.
```


**dp[i]代表最少0-i个字符最少需要切几刀变回文**

把一个字符串分成j, j + 1 ~ i，

保证j + 1 ~ i是回文，求f(j)的最小分割数，最后加上最后一刀1
* s(j~i)回文    dp[i] = min(dp[i],dp[j] + 1)
* 注意初始化dp[i] = i - 1,表示最多割几刀  dp[0]就是-1刀 这样才能比较！


naive solution:

O(n^3)

```java
public class Solution {
    //dp[s.length]
    //j+1- i回文 dp[i] = dp[j] + 1
    public int minCut(String s) {
        if (s == null && s.length() == 0) return 0;
        
        int[] dp = new int[s.length() + 1];
        for (int i = 0; i <= s.length(); i++) {
            dp[i] = i - 1;
        }
        
        
        for (int i = 1; i <= s.length(); i++) {
            for (int j = i - 1; j >= 0; j--) {
                if (isPal(s.substring(j, i))) {
                    dp[i] = Math.min(dp[i], dp[j] + 1);
                }
            }
        }
        
        return dp[s.length()];
    }
    
    private boolean isPal(String s) {
        int start = 0;
        int end = s.length() - 1;
        while (start < end) {
            if (s.charAt(start) == s.charAt(end)) {
                start++; 
                end--;
                continue;
            } else {
                return false;
            }
        }
        
        return true;
    }
}
```

Best Solution:

O(n^2)
* 二刷时候没想清楚区间动归的初始化长度 这里初始化为string length方便和charAt的index一起比较
* 区间动归的for loop很有特色 第一层**for len**, 第二层for start，这杨才能保证start不越界并且慢慢增加区间长度


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