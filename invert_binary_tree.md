# Invert Binary Tree

思路:

递归：  
要翻转二叉树就必须先翻转二叉树的左右子树，由此想到分治递归的方法  
递归得到翻转好的左子树和翻转的右子树，再交换左右子树

非递归：  
BFS加入queue,加入queue前先交换左右子树

分治 O\(n\)  O\(h\)

```java
public TreeNode invertTree(TreeNode root) {
    if (root == null) {
        return null;
    }
    TreeNode right = invertTree(root.right);
    TreeNode left = invertTree(root.left);
    root.left = right;
    root.right = left;
    return root;
}
```

BFS遍历 O\(n\) O\(n\)

```java
public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;

        Queue<TreeNode> queue = new LinkedList<>();

        queue.offer(root);

        while(!queue.isEmpty()) {
            TreeNode curr = queue.poll();
            TreeNode tmp = curr.left;
            curr.left = curr.right;
            curr.right = tmp;

            if (curr.left != null) queue.offer(curr.left);
            if (curr.right != null) queue.offer(curr.right);

        }

        return root;
    }
```



