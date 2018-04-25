# Symmetric Tree

[https://leetcode.com/problems/symmetric-tree/description/](https://leetcode.com/problems/symmetric-tree/description/)

![](/assets/1.png)要求递归+非递归 都是O\(n\)

递归：分治的思想

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;

        return helper(root.left, root.right);
    }

    private boolean helper(TreeNode left, TreeNode right) {
        if (left == null || right == null) {
            return left == right;
        }

        if (left.val != right.val) return false;
        return helper(left.left, right.right) && helper(left.right, right.left);
    }
}
```

非递归: level order traversal + 双队列比较

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        
        Queue<TreeNode> q1 = new LinkedList<>();
        Queue<TreeNode> q2 = new LinkedList<>();
        
        q1.offer(root.left);
        q2.offer(root.right);
        
        while (!q1.isEmpty() && !q2.isEmpty()) {
            TreeNode n1 = q1.poll();
            TreeNode n2 = q2.poll();
            
            if (n1 == null && n2 == null) continue;
            if (n1 == null || n2 == null) return false;
            if (n1.val == n2.val) {
                q1.offer(n1.left);
                q2.offer(n2.right);
                q1.offer(n1.right);
                q2.offer(n2.left);
            } else {
                return false;
            }
        }
        
        return true;
    }
}
```



