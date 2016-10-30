# Unique BST (DP)

![](Screen Shot 2016-10-30 at 5.19.19 PM.png)


分析：
* 选取一个结点为根，就把结点切成左右子树，以这个结点为根的可行二叉树数量就是左右子树可行二叉树数量的乘积
* 总的数量是将以所有结点为根的可行结果累加起来
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