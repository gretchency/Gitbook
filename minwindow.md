# MinWindow

```java
//给个list of words 求s最少能包货这些word的window
//先把t录入map 左右指针转s，右指针先走 减map 加count count== length时有第一个window 此时走左看看能不能缩
public class MinWindow {
    public String minWindow(String s, List<String> t) {
        StringBuilder sb = new StringBuilder();
        for (String word: t) {
            sb.append(word);
        }
        
        String dest = sb.toString();
        HashMap<Character, Integer> map = new HashMap<>();
        for (int i = 0; i < dest.length(); i++) {
            if (!map.containsKey(dest.charAt(i))) {
                map.put(dest.charAt(i), 1);
            } else {
                map.put(dest.charAt(i), map.get(dest.charAt(i)) + 1);
            }
        }
        
        
        int left = 0;
        int right = 0;
        int minLen = Integer.MAX_VALUE;
        int index = 0;
        int count = 0;
        
        while (left < s.length() && right < s.length()) {            
            char rc = s.charAt(right);
            if (map.containsKey(rc)) {
                map.put(rc, map.get(rc) - 1);
                
                if (map.get(rc) >= 0) {
                    count++;
                    while (count == dest.length()) {
                        minLen = Math.min(minLen, right - left + 1);
                        index = left;
                        char lc = s.charAt(left);
                        if (map.containsKey(lc)) {
                            map.put(lc, map.get(lc) + 1);
                            
                            if (map.get(lc) > 0) count--;
                        }
                        left++;
                    }
                }
            }
            
            right++;
        }
        
        if (minLen != Integer.MAX_VALUE) {
            return s.substring(index, index + minLen);
        } else {
            return "";
        }
    }

    public static void main(String[] args) {
        MinWindow minw = new MinWindow();
        List<String> test = new ArrayList<>();
        test.add("AB");
        test.add("C");
        //System.out.println("TEST");
        System.out.println(minw.minWindow("ABANC", test));
        //System.out.println("TEST2");

    }

}
```