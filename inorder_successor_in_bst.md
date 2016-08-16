# Inorder successor in BST


successor变量记录root的父亲结点，当while循环结束时，如果原本的root = Null或者p不存在与BST中(那么此刻root = null)，都返回Null

找到p之后，如果p没有右儿子，则第一个比它大的数字就是刚刚记录的successor

找到p之后，如果有右儿子，则找到右子树中的最左边的值(最小值)

```java
public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {

    TreeNode successor = null;
    
    //两个终止条件，一个是没找到，一个是找到p
    while(root != null && root.val != p.val) {
        if (root.val > p.val) {
            successor = root;
            root = root.left;
        } else {
            root = root.right;
        }
    }
    
    //原本的root = null 或者 p不存在与BST中，此刻root = null
    if (root == null) return null;
    
    //找到p之后，如果p没有右儿子，则第一个比它大的数字就是刚刚记录的successor
    if (root.right == null) return successor;
    
    //p有右儿子，则找到右子树中的最左边的值（最小值）
    root = root.right;
    while (root.left != null) {
        root = root.left;
    }
    
    return root;
}
```