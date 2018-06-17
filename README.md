# My Awesome Book

仅供本人学习算法数据结构之用，是我自己的参考书，一切引用需要注释请提醒我。

```java
class Solution {
    private int maxSum = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        helper(root);
        return maxSum;
    }
    
    private int helper(TreeNode root) {
        if (root == null) return 0;
        int left = helper(root.left);
        int right = helper(root.right);
        int returnToParent = Math.max(root.val, Math.max(root.val + left, root.val + right));
        maxSum = Math.max(maxSum, Math.max(returnToParent, root.val + left + right));
        return returnToParent;
    }
}
```



