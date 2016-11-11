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

还有一种只告诉目标Node的情况，这时候需要parent node来找到successor

```java
public static TreeNode getSuccessor(TreeNode node) {
        //node有右子树,找右子树里最左点
        if (node.right != null) {
            TreeNode res = getMin(node.right);
            return res;
        }
        
        //找parent里第一个比node大的
        TreeNode parent = node.parent;
        while (parent != null && parent.val < node.val) {
            parent = parent.parent;
        }
        return parent;
    }
    
    private static TreeNode getMin(TreeNode node) {
        while (node.left != null) {
            node = node.left;
        }
        return node;
    }
```
