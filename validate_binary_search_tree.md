# Validate Binary Search Tree

增改删查的复杂度都是O\(h\)

O\(log\(n\)\)是平衡二叉树的复杂度

```java
1
  \
    4
      \
       6
```

二刷

* 用Long防止数字很大无法比较
* 非递归 就是inorder一遍 同样用long防止溢出

```java
    public boolean isValidBST(TreeNode root) {
        if (root == null) return true;

        TreeNode curr = root;
        Stack<TreeNode> stack = new Stack<>();

        //pre用long
        long pre = Long.MIN_VALUE;
        while (curr != null || !stack.isEmpty()) {
            while(curr != null) {
                stack.push(curr);
                curr = curr.left;
            }
            curr = stack.pop();
            if (curr.val > pre) {
                pre = curr.val;
            } else {
                return false;
            }
            curr = curr.right;
        }
        return true;
    }
```

### 时间复杂度：O\(n\) 空间：O\(n\)

* 遍历各个节点一次
* 用到stack存放TreeNode

```java
    public boolean isValidBST(TreeNode root) {
        if (root == null) return true;

        return helper(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public boolean helper(TreeNode node, long min, long max) {
        if (node == null) {
            return true;
        }

        if (node.val <= min || node.val >= max) return false;

        return helper(node.left, min, node.val) && helper(node.right, node.val, max);
    }
```

### 时间复杂度：O\(n\)

* 递归遍历所有节点各一次

左根右递增 递归整棵树 看min 和 max是否fit in

```java
public boolean isValidBST(TreeNode root) {
        //一定要用Long
        return helper(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public boolean helper(TreeNode node, long min, long max) {
        //终止条件
        if (node == null) {
            return true;
        }

        if (node.val <= min || node.val >= max {
            return false;
        }

        //左根右递增 左<根 右>根
        return helper(node.left, min, node.val) && helper(node.right, node.val, max);
    }
```



