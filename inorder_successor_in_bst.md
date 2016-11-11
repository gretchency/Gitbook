# Inorder successor in BST


BST 里面，任意位置，任意楼层，都可以通过 value 的比较确定相对位置，这是 BST 一个最好用的性质。

因此在 BST 里面，确定起来就很简单了，从 root 往下走，每次往左拐的时候，存一下，记录着最近一个看到的比 p.val 大的 node 就行了。

```java
public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (root == null) return null;
        TreeNode res = null;
        while (root != null) {
            if (root.val > p.val) {
                res = root;
                root = root.left;
            } else {
                root = root.right;
            }
        }
        
        return res;
    }
```

递归：

```
public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
    if (root == null) {
        return root;
    }

    if (root.val <= p.val) {
        return inorderSuccessor(root.right, p);
    } else {
        TreeNode left = inorderSuccessor(root.left, p);
        return left != null ? left : root;
    }
}
```

Presuccessor
```java
public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (root == null) return null;
        TreeNode res = null;
        while (root != null) {
            if (root.val > p.val) {
                root = root.left;
            } else {
                res = root;
                root = root.right;
            }
        }
        
        return res;
    }
```
