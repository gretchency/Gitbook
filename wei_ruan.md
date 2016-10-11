# 微软On Campus

Validate Binary Search Tree

当时脑子抽了，直接递归了，只比较了左子树和右子树里元素是否满足BST，没比较root value.

**错解！！**
```java
    public boolean isValidBST(TreeNode root) {
        // write your code here
        if (root == null) return true;
        
        if (root.left != null && root.val <= root.left.val) return false;
        if (root.right != null && root.val >= root.right.val) return false;
        return isValidBST(root.left) && isValidBST(root.right);
    }
```



```java
public boolean isValidBST(TreeNode root) {
        // write your code here
        if (root == null) return true;
        
        return helper(root, Long.MIN_VALUE, Long.MAX_VALUE);
        
    }
    
    public boolean helper(TreeNode root, long min, long max) {
        if (root == null) return true;
        
        if (root.val <= min || root.val >= max) return false;
        
        return helper(root.left, min, root.val) && helper(root.right, root.val, max);
    }
```