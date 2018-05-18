Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

**Example: **

```
You may serialize the following tree:

    1
   / \
  2   3
     / \
    4   5

as 
"[1,2,3,null,null,4,5]"
```

**Clarification:**Just the same as[how LeetCode OJ serializes a binary tree](https://leetcode.com/faq/#binary-tree). You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Note: **Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.



思路

序列化用preorder travesal存储序列，反序列化时候也用preorder traversal解密，反序列化时候用到一个Queue来poll最前面的数

时间复杂度: `O(n)`

空间复杂度: 用到了一个Queue `O(n)`



```java
public class Codec {
    private static final String SPLITER = ",";
    private static final String NULL = "x";

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if (root == null) return null;
        
        StringBuilder sb = new StringBuilder();
        buildString(sb, root);
        return sb.toString();
    }
    
    private void buildString(StringBuilder sb, TreeNode root) {
        if (root == null) {
            sb.append(NULL).append(SPLITER);
            return;
        }
        
        sb.append(root.val).append(SPLITER);
        buildString(sb, root.left);
        buildString(sb, root.right);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data == null) return null;
        Queue<String> q = new LinkedList<>();
        q.addAll(Arrays.asList(data.split(SPLITER)));
        return buildTree(q);
    }
    
    private TreeNode buildTree(Queue<String> q) {
        String val = q.poll();
        if (val.equals(NULL)) return null;
        
        TreeNode root = new TreeNode(Integer.valueOf(val));
        root.left = buildTree(q);
        root.right = buildTree(q);
        return root;
    }
}

```



