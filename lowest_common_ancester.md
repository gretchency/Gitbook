# Lowest Common Ancester

http://www.lintcode.com/en/problem/lowest-common-ancestor/


不告诉Parent节点，自顶向下，分治的解法。



```java
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode A, TreeNode B) {
        //若root上有A或B,返回root
        if (root == null || root == A || root == B) {
            return root;
        }
        
        TreeNode left = lowestCommonAncestor(root.left, A, B);
        TreeNode right = lowestCommonAncestor(root.right, A, B);
        //A,B分居左右，祖先root
        //左边有A,B，返回左
        //右边有A,B, 返回右
        if (left != null && right != null) {
            return root;
        }
        
        if (left != null) {
            return left;
        }
        
        if (right != null) {
            return right;
        }
        
        return null;
    }
```

告诉Parent节点

两个ArratList存A,B到root路径，从后往前比，取到最近的公共祖先


```java
    private ArrayList<TreeNode> getPath2Root(TreeNode node) {
        ArrayList<TreeNode> list = new ArrayList<TreeNode>();
        if (node != null) {
            list.add(node);
            node = node.parent;
        }
        
        return list;
    }
    
    public TreeNode lowestCommonAncester(TreeNode A, TreeNode B) {
        ArrayList<TreeNode> list1 = getPath2Root(A);
        ArrayList<TreeNode> list2 = getPath2Root(B);
        
        int i = list1.size() - 1, j = list2.size() - 1;
        
        for(i, j; i >= 0 && j >= 0; i--, j--) {
            if (list1.get(i) != list2.get(j)) 
                //取到第一个不一样的Parent节点
                return list1.get(i + 1);
            }
        }
        
        return list1.get(i + 1);
    }
```
