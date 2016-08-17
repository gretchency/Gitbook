# Binary Tree Preorder Treversal

http://www.lintcode.com/en/problem/binary-tree-preorder-traversal/#

递归
```java
    public ArrayList<Integer> preorderTraversal(TreeNode root) {
        ArrayList<Integer> result = new ArrayList<Integer>();
        traverse (root, result);
        return result;
    }
    
    private void traverse(TreeNode root, ArrayList<Integer> result) {
        if (root == null) return;
        //根左右
        result.add(root.val);
        traverse(root.left, result);
        traverse(root.right, result);
    }
```

非递归

先把根Push进去

result记录结果

**While stack不为空，pop,push right,push left
**

**注意while里先push右子树，再push左子树（stack 先进后出）
**
```java
public ArrayList<Integer> preorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        ArrayList<Integer> result = new ArrayList<Integer>();
        if (root == null) return result;

        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            result.add(node.val);
            if (node.right != null) {
                stack.push(node.right);
            }
            
            if (node.left != null) {
                stack.push(node.left);
            }
        }
        
        return result;
    }
```

Inorder

 Binary Search Tree Iterator
 
 http://www.lintcode.com/en/problem/binary-search-tree-iterator/
 
 ```java
 public class BSTIterator {
    private TreeNode curr;
    private Stack<TreeNode> stack = new Stack<TreeNode>();
    //@param root: The root of binary tree.
    public BSTIterator(TreeNode root) {
        curr = root;
    }

    //@return: True if there has next node, or false
    public boolean hasNext() {
        return (curr != null || !stack.isEmpty());
    }
    
    //@return: return next node
    public TreeNode next() {
    //先一直压左，然后 到底了就pop, 加入结果， 最后往右

        while(curr != null) {
            stack.push(curr);
            curr = curr.left;
        }
        curr = stack.pop();
        TreeNode node = curr;
        curr = curr.right;
        
        return node;
    }
}
 ```