# Longest Substring Without Repeating Characters

![](Screen Shot 2016-10-25 at 10.19.18 PM.png

* 滑动窗口法（end:橘色指针，start蓝色指针）
* 256 boolean数组存储访问状态
* 先滑end，走到划不动，开始滑start,全都变为false，直到能滑动为止，每次更新maxLen
* start + len = s.length()就可以停止了



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