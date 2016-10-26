# House Robber III
[House Robber III](https://leetcode.com/problems/house-robber-iii/)

小偷在二叉树上作案，不能偷相邻两个节点，只能隔着偷，问最大偷多少？

思路：
* 还是类比House RobberI II,分成偷当前节点和不偷当前节点两种情况，然后比较哪个大。
  * 需要维护两个元素的res数组，分别是有root的最大值和没root的最大值
  * dfs分治求left,right,和root节点比较求解出最大情况
```java
public class Solution {
    public int rob(TreeNode root) {
        if (root == null) return 0;
        
        //第一个元素:包含该节点结果，第二：不包含该节点结果
        int[] res = new int[2];
        
        res = dfs(root);
        
        return Math.max(res[0], res[1]);
    }
    
    private int[] dfs(TreeNode root) {
        if (root == null) return new int[2];
        
        int[] left = dfs(root.left);
        int[] right = dfs(root.right);
        
        int[] res = new int[2];
        //包含root，那么不包含相邻点
        res[0] = left[1] + root.val + right[1];
        //不包含root，那么可以包含相邻点
        res[1] = Math.max(left[0], left[1]) + Math.max(right[0], right[1]);
        return res;
    }
}
```