# Regular Expression Match

tag: Snapchat

Implement regular expression matching with support for '.' and '*'.
'.' Matches any single character. '*' Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).

Some examples:
```
 isMatch("aa","a") → false
 isMatch("aa","aa") → true
 isMatch("aaa","aa") → false
 isMatch("aa", "a*") → true
 isMatch("aa", ".*") → true
 isMatch("ab", ".*") → true
 isMatch("aab", "c*a*b") → true
```

## **递归：**
* 递归比较每一位，逐步缩减s，看能不能缩到为空，同时p也为空或*串
* 如果第一位相等且p的第二位是```星号```，要分两种情况：使用该符号吃s字符或是跳过符号，比p的第三位。

```java
public class Solution {
    public boolean isMatch(String s, String p) {
        if (s.length() == 0) {
            return checkEmpty(p);
        }
        
        if (p.length() == 0) return false;
        
        char s1 = s.charAt(0);
        char p1 = p.charAt(0);
        char p2 = '0';
        
        if (p.length() > 1) {
            p2 = p.charAt(1);
        }
        
        if (p2 == '*') {
            if (compare(s1, p1)) {
                //分两种情况，用或是不用p1*,
                //如果用，可以先吃掉s的第一个字母，接着看能不能吃掉其他的
                //不用的话就相当于p1*没吃掉s任何字母，跳过前两位，接着看p第三位
                return isMatch(s.substring(1), p) || isMatch(s, p.substring(2));
            } else {
                return isMatch(s, p.substring(2));
            }
            
        } else {
            if (compare(s1, p1)) return isMatch(s.substring(1), p.substring(1));
            return false;
        }
    }
    
    private boolean compare(char a, char b) {
        return a == b || a == '.' || b == '.';
    }
    
    //如果奇数长度肯定有不是p1*组合的
    //偶数位一定要是*才算empty
    private boolean checkEmpty(String p) {
        if (p.length() % 2 != 0) return false;
        
        for (int i = 1; i < p.length(); i += 2) {
            if (p.charAt(i) != '*') return false;
        }
        
        return true;
    }
}
```


## DP优化：
* dp[i][j]代表p(0~i-1)是否能match s(0~j-1)
* 初始化时要把p*p*p*这种时dp[i][0]设为true
* 当最后一位是*,倒数第二位和s最后一位相同时分情况讨论
  * dp[i][j] = dp[i - 2][j] || dp[i][j - 1]

```java
public class Solution {
    public boolean isMatch(String s, String p) {
        if (s == null || p == null) return false;
        
        int m = p.length();
        int n = s.length();
        //dp[i][j] stands for (0, i - 1) p can eat (0, j-1)s
        boolean[][] dp = new boolean[m + 1][n + 1];
        
        dp[0][0] = true;
        for (int i = 2; i <= m; i++) {
            //like p*p*p*
            if (p.charAt(i - 1) == '*' && dp[i - 2][0]) dp[i][0] = true;
        }
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (p.charAt(i - 1) == '*') {
                    //不等就要消耗p
                    if (!compare(p.charAt(i - 2), s.charAt(j - 1))) {
                        dp[i][j] = dp[i - 2][j];
                    } else {//相等的话可以选择用或不用p
                        dp[i][j] = dp[i - 2][j] || dp[i][j - 1];
                    }
                } else {
                    if (compare(p.charAt(i - 1), s.charAt(j - 1))) {
                        dp[i][j] = dp[i - 1][j - 1];
                    } else {
                        dp[i][j] = false;
                    }
                }
            }
        }
        
        return dp[m][n];
        
    }
    
    private boolean compare(char a, char b) {
        return a == b || a == '.';
    }
}
```


