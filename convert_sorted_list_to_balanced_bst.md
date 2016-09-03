# Convert Sorted List to Balanced BST

O(n)

```java
public class Solution {
    /**
     * @param head: The first node of linked list.
     * @return: a tree node
     */
    
    //维护一个全局变量curr
    private ListNode curr;
     
    public int getSize(ListNode head) {
        int size = 0;
        while (head != null) {
            size++;
            head = head.next;
        }
        return size;
    }
    
    public TreeNode sortedListToBST(ListNode head) {  
        if (head == null) {
            return null;
        }
        
        int size = getSize(head);
        curr = head;
        return sortedListToBSTHelper(size);
    }
    
    private TreeNode sortedListToBSTHelper(int size) {
        if (size <= 0) return null;
        
        TreeNode left = sortedListToBSTHelper(size / 2);
        TreeNode root = new TreeNode(curr.val);
        curr = curr.next;
        //减掉左子树和根节点
        TreeNode right = sortedListToBSTHelper(size - size / 2 - 1);
        
        root.left = left;
        root.right = right;
        
        return root;
    }
}
```