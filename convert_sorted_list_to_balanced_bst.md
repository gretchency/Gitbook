# Convert Sorted List to Balanced BST
二刷

分治递归：类比Convert sorted array,想到要找到list的中点，要知道list中点必须要知道list的长度。所以可以传入长度和头节点来递归，每次递归通过长度一半遍历得到中间节点，然后根据中间节点分治左右子数 
* 注意递归的base case:```if (head == null || len == 0) return null;```
* 注意根据长度求中点时 curr < len / 2  可以想例子 比如长度是4时，可以取第2或者3的点，那么curr从0开始可以到2，然后跳出循环，所以curr < len / 2


```java
public class Solution {
    private int findLen(ListNode head) {
        int len = 0;
        
        ListNode curr = head;
        while (curr != null) {
            curr = curr.next;
            len++;
        }
        return len;
    }
    
    public TreeNode sortedListToBST(ListNode head) {
        if (head == null) return null;
        
        int len = findLen(head);
        return helper(head, len);
    }
    
    private TreeNode helper(ListNode head, int len) {
        if (head == null || len == 0) return null;
        
        int count = 0;
        ListNode curr = head;
        while (count < len / 2) {
            curr = curr.next;
            count++;
        }
        
        TreeNode root = new TreeNode(curr.val);
        
        root.left = helper(head, len / 2);
        root.right = helper(curr.next, len - len / 2 - 1);
        
        return root;
    }
}

```







O(n)

分治的思想
curr做根节点 慢慢往后挪


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