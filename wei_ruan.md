# 微软On Campus

1. Validate Binary Search Tree

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

2. Set Matrix Zero
三种解法可以优化空间
naive O(mn)
basic O(m + n)
perfect O(1)

飞快写出basic以后优化时候蒙蔽了，没往O(1)处想。

面试官最后提示说用HashSet，其实也没要求O(1)空间。

空间O(1)解法

```java
public class Solution {
    public void setZeroes(int[][] matrix) {
        if (matrix == null || matrix.length == 0) return;
        int m = matrix.length;
        int n = matrix[0].length;
        
        boolean flagRow = false;
        boolean flagCol = false;
        
        //先标记第0行第0列是否含0
        for (int i = 0; i < m; i++) {
            if (matrix[i][0] == 0) {
                flagRow = true;
                break;
            }
        }
        
        for (int j = 0; j < n; j++) {
            if (matrix[0][j] == 0) {
                flagCol = true;
                break;
            }
        }
        
        
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }
        
        
        //先不管第0行第0列 i 和 j都从1开始考虑
        for (int i = 1; i < m; i++) {
            if (matrix[i][0] == 0) {
                for (int j = 1; j < n; j++) {
                    matrix[i][j] = 0;
                }
            }
        }
        
        for (int j = 1; j < n; j++) {
            if (matrix[0][j] == 0) {
                for (int i = 1; i < m; i++) {
                    matrix[i][j] = 0;
                }
            }
        }
        
        //最后考虑第0行第0列
        if (flagRow == true) {
            for (int i = 0; i < m; i++) {
                matrix[i][0] = 0;
            }
        }
        
        if (flagCol == true) {
            for (int j = 0; j < n; j++) {
                matrix[0][j] = 0;
            }
        }
        
        return;
    }
}
```