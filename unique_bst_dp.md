# Unique BST (DP)

![](Screen Shot 2016-10-30 at 5.19.19 PM.png)

```java
public class Solution {
    public int numTrees(int n) {
        if (n < 0) return -1;
        int[] count = new int[n + 1];
        count[0] = 1;
        count[1] = 1;
        for (int i = 2; i <= n; i++) {
            for (int j = 0; j < i; j++) {
                count[i] += count[j] * count[i - j - 1];
            }
        }
        
        return count[n];
    }
}
```