# Maximum Depth of Binary Tree
http://www.lintcode.com/en/problem/maximum-depth-of-binary-tree/

**分治和普通递归的区别**：分治一般helper函数会return东西，而普通递归一般都是void方法



**普通递归**

用全局变量记录深度，helper函数currDepth更新深度，一旦curr>depth,更新depth

时间复杂度：O(n) 每个点都访问一次

```java
    //全局变量记录深度
    private int depth;
    public int maxDepth(TreeNode root) {
        depth = 0;
        helper(root, 1);
        
        return depth;
    }
    
    private void helper(TreeNode node, int currDepth) {
        if (node == null) return;
        //一旦currDepth大于depth，更新depth
        if (currDepth > depth) {
            depth = currDepth;
        }
        
        helper (node.left, currDepth + 1);
        helper (node.right, currDepth + 1);
    }
```


**分治**

Divide and Conquer, 左右子树最大高度，再加根节点的一

```java
    public int maxDepth(TreeNode root) {
        // Divide and Conquer, 左右子树最大高度，再加一
        if (root == null) {
            return 0;
        }
        
      int left = maxDepth(root.left);
      int right = maxDepth(root.right);
       
      return Math.max(left, right) + 1;
    }
```

Related Problems:

**Minimum Depth of Binary Tree
**http://www.lintcode.com/en/problem/minimum-depth-of-binary-tree/

一定要判断左右子树为空的情况，若为空 只比另一边子树

因为子树为空并不是说该子树为最小深度
```java
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        int left = minDepth(root.left);
        int right = minDepth(root.right);
        
        //****一定要判断左右子树为空的情况，若为空 只比另一边子树
        if (root.left == null) {
            return right + 1;
        }
        
        if (root.right == null) {
            return left + 1;
        }
        return Math.min(left, right) + 1;
    
    }
```

 Balanced Binary Tree

http://www.lintcode.com/en/problem/balanced-binary-tree/
```java
public boolean isBalanced(TreeNode root) {
        if (root == null) return true;
        //左右子树是否平衡
        if (!isBalanced(root.left) || !isBalanced(root.right)) {
            return false;
        }
        //左右子树高度差
        int dif = getHeight(root.left) - getHeight(root.right);
        
        return dif >= -1 && dif <= 1;
         
        
    }
    
    private int getHeight(TreeNode node) {
        if (node == null) return 0;
        int left = getHeight(node.left);
        int right = getHeight(node.right);
        
        return Math.max(left, right) + 1;
    }
```