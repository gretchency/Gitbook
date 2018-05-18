![](/assets/import5.png)思路

level order traversal 但是用到了额外空间

时间复杂度: `O(n)`

空间复杂度：`O(2 ^ (height))`

```java
public class Solution {
    public void connect(TreeLinkNode root) {
        if (root == null) return;
        
        Queue<TreeLinkNode> q = new LinkedList<>();
        q.offer(root);
        
        while (!q.isEmpty()) {
            List<TreeLinkNode> list = new ArrayList<>();
            int size = q.size();
            for (int i = 0; i < size; i++) {
                TreeLinkNode curr = q.poll();
                if (i < size - 1) {
                    curr.next = q.peek();
                } 
                if (curr.left != null) {
                    q.offer(curr.left);
                }
                if (curr.right != null) {
                    q.offer(curr.right);
                }
            }
        }
    }
}
```

先序遍历一遍，把连接条件构造好

时间复杂度：`O(n)`

空间复杂度：`O(h)`

```java
public class Solution {
    public void connect(TreeLinkNode root) {
        if (root == null || root.left == null || root.right == null) return;
        
        root.left.next = root.right;
        if (root.next != null) {
            root.right.next = root.next.left;
        }
        
        connect(root.left);
        connect(root.right);
    }
}
```



