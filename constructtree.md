# ConstructTree


给一个前序数组 和 中序数组 构造bst
```java
public class ConstructTree {
    
    public TreeNode construct(int[] preorder, int[] inorder) {
        //map存一下每个inorder element的index
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }
        
        return helper(preorder, inorder, 0, preorder.length - 1, 0, inorder.length - 1, map);
    }
    
    public TreeNode helper(int[] preorder, int[] inorder, int prestart, int preend, int instart, int inend, Map<Integer, Integer> map) {
        if (prestart > preend || instart > inend) return null;
        
        int rootVal = preorder[prestart];
        TreeNode root = new TreeNode(rootVal);
        
        int index = map.get(rootVal);
        int leftPre = index - instart;
        
        root.left = helper(preorder, inorder, prestart + 1, prestart + leftPre, instart, index - 1, map);
        root.right = helper(preorder, inorder, prestart + leftPre + 1, preend, index + 1, inend, map);
        
        return root;
    }

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        ConstructTree ct = new ConstructTree();
        int[] a = new int[]{1,3,2,4,5};
        int[] b = new int[]{2,3,4,1,5};
        System.out.println(ct.construct(a, b).val);
    }

}


class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    public TreeNode(int val) {
        this.val = val;
    }
}
```