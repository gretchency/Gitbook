# Binary Tree Maximum Path Sum 简单 难

简单：root到某个节点的最大path

分治 左右子树的最大Path求出后，和0比一下， 最后再加上根

![](Screen Shot 2016-08-11 at 3.59.29 PM.png)

```java
    public int maxPathSum(TreeNode root) {
        if (root == null) {
            return Math.MIN_VALUE;
        }
        
        int left = maxPathSum(root.left);
        int right = maxPathSum(root.right);
        
        //如果不和0比，就是root到每个叶子节点的最长路径，因为左右子数可能<0，此时要砍掉，只输出root.val
        return Math.max(Math.max(left, right), 0) + root.val;
    }
```

难
any node to any node



![](Screen Shot 2016-08-11 at 4.16.10 PM.png)
分析：
https://algorithm.yuanbin.me/zh-hans/binary_tree/binary_tree_maximum_path_sum.html

也可用max[]避免全局变量。就是一个存result的reference object，java不支持c++那种直接&传reference

    int[] max = new int[1];


```java
public class Solution {
    //全局变量maxValue记录全局最大和
    //递归函数返回root的子树到root节点(含)路径长度的最大值
    //巧妙利用0。若子树和为负，则取值0
    int maxValue;
    public int maxPathSum(TreeNode root) {
        if (root == null) return Integer.MIN_VALUE;
        
        maxValue = Integer.MIN_VALUE;
        maxPathDown(root);
        
        return maxValue;
    }
    
    private int maxPathDown(TreeNode root) {
        if (root == null) return 0;
        
        int left = Math.max(0, maxPathDown(root.left));
        int right = Math.max(0, maxPathDown(root.right));
        maxValue = Math.max(maxValue, left + right + root.val);
        
        return Math.max(left, right) + root.val;
    }
}
```

