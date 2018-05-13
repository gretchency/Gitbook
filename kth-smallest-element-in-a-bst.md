Given a binary search tree, write a function`kthSmallest`to find the**k**th smallest element in it.

**Note:**  
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

**Example 1:**

```
Input:
 root = [3,1,4,null,2], k = 1

Output:
 1
```

**Example 2:**

```
Input:
 root = [5,3,6,2,4,null,null,1], k = 3

Output:
 3
```

**Follow up:**  
What if the BST is modified \(insert/delete operations\) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?



思路：

非递归inorder traversal 整个BST，用一个index记录traversal到第几个了，到第k个时候输出结果

时间复杂度:`O(k)`

空间复杂度:`O(h)`, h为bst的高度

```java
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        if (root == null) return -1;
        return inorderHelper(root, k);
    }

    private int inorderHelper(TreeNode root, int k) {
        Stack<TreeNode> stack = new Stack<>();
        pushToLeft(stack, root);
        int index = 0;
        while (!stack.isEmpty()) {
            TreeNode curr = stack.pop();
            index++;
            if (index == k) return curr.val;
            if (curr.right != null) {
                pushToBottom(stack, curr.right);
            }
        }

        return -1;
    }

    private void pushToLeft(Stack<TreeNode> stack, TreeNode root) {
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
    }
}
```



