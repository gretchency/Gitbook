# Validate Binary Search Tree

增改删查的复杂度都是O(h)

O(log(n))是平衡二叉树的复杂度

```java
1
  \
    4
      \
       6
```


左根右递增 递归整棵树 看min 和 max是否fit in
```java
public boolean isValidBST(TreeNode root) {
        //先给两个null
        return helper(root, null, null);
    }
    
    public boolean helper(TreeNode node, Integer max, Integer min) {
        //终止条件
        if (node == null) {
            return true;
        }
        
        //一定要判断是否null
        if ((min != null && node.val <= min) || (max != null && node.val >= max)) {
            return false;
        }
        
        //左根右递增 左<根 右>根
        return helper(node.left, node.val, min) && helper(node.right, max, node.val);
    }
```