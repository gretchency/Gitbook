```java
public class Solution {
    /**
     * @param s: A string s
     * @param dict: A dictionary of words dict
     */
    public boolean wordBreak(String s, Set<String> dict) {
        //state
        boolean[] dp = new boolean[s.length() + 1];

        //init
        dp[0] = true;

        //get max len
        int maxLen = Integer.MIN_VALUE;

        for(String a: dict) {
            if (a.length() > maxLen) {
                maxLen = a.length();
            }
        }



        //function
        //注意最大单词长度不可能超过dictionary里的最长单词，可以优化复杂度
        for (int i = 1; i <= s.length(); i++) {
            for (int j = i - 1; j >= 0 && i - j <= maxLen; j--) {
                String word = s.substring(j, i);
                if (dp[j] & dict.contains(word)) {
                    dp[i] = true;
                    break;
                }
            }
        }

        //answer
        return dp[s.length()];
    }
}
```



