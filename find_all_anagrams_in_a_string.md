# Find all anagrams in a String

![](Screen Shot 2016-10-29 at 9.18.02 PM.png)

```java
public class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> res = new ArrayList<>();
        
        int[] h1 = new int[256];
        int[] h2 = new int[256];
        
        int m = s.length();
        int n = p.length();
        
        for (int i = 0; i < n; i++) {
            h2[p.charAt(i)]++;
        }
        
        for (int i = 0; i < m; i++) {
            h1[s.charAt(i)]++;
            if (i >= n) {
                h1[s.charAt(i - n)]--;
            }
            if (Arrays.equals(h1, h2)) res.add(i - n + 1);
        }
        
        return res;
    }
}
```