# Longest Substring Without Repeating Characters

![](Screen Shot 2016-10-25 at 10.19.18 PM.png

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        boolean[] exist = new boolean[256];
        
        int end = 0;
        int start = 0;
        int res = 0;
        
        while (end < s.length() && start + res < s.length()) {
            if (!exist[s.charAt(end)]) {
                exist[s.charAt(end++)] = true;
            } else {
                exist[s.charAt(start++)] = false;
            }
            
            res = Math.max(res, end - start);
        }
        
        return res;
    }
}
```