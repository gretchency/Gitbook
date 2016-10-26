# Minimum Window Substring

双指针解决
* 先根据t建立map,key是字母，value是该字母出现了几次
* 右指针先走，满足就减value,先找到满足条件的一个窗口，更新MinLen,左指针开始走，看看能不能缩小窗口，一直走到不满足条件，这时候右指针接着走，来满足左指针挖下的坑，以此类推。
* value为非负就增加Count,为负说明减多了，这时候用left指针增，直到为正时候说明又缺这一字母了。


```java
public class Solution {
    public String minWindow(String s, String t) {
        if (s == null || t == null || s.length() < t.length()) return "";
        
        
        Map<Character, Integer> map = new HashMap<>();
        for (int i = 0; i < t.length(); i++) {
            char c = t.charAt(i);
            if (map.containsKey(c)) {
                map.put(c, map.get(c) + 1);
            } else {
                map.put(c, 1);
            }
        }
        
        int right = 0;
        int left = 0;
        //用来计算满足了t里几个字母
        int count = 0;
        //用来存储当前最小len的头index
        int minIndex = 0;
        int minLen = Integer.MAX_VALUE;
        while (right < s.length() && left < s.length()) {
            char rc = s.charAt(right);
            if (map.containsKey(rc)) {
                map.put(rc, map.get(rc) - 1);
                if (map.get(rc) >= 0) count++;
                while (count == t.length()) {
                    if (minLen > right - left + 1) {
                        minLen = right - left + 1;
                        minIndex = left;
                    }
                    char lc = s.charAt(left);
                    if (map.containsKey(lc)) {
                        map.put(lc, map.get(lc) + 1);
                        if (map.get(lc) > 0) count--;
                    }
                    
                    left++;
                }
            }
            right++;
        }
        
        if (minLen != Integer.MAX_VALUE) {
            return s.substring(minIndex, minIndex + minLen);
        } else {
            return "";
        }
    }
}
```