# Convert Sorted List to Balanced BST

三刷（暴力解）

自顶向下的方法，先找到root然后对左右子树分别递归调用。

快慢指针找中点建树递归

```java
public TreeNode sortedListToBST(ListNode head) {
        // write your code here
        if (head == null) return null;

        ListNode fast = head;
        ListNode slow = head;
        ListNode prev = null;

        while (fast.next != null && fast.next.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }

        if (prev != null) {
            prev.next = null;
        } else {
            head = null;
        }

        TreeNode root = new TreeNode(slow.val);
        root.left = sortedListToBST(head);
        root.right = sortedListToBST(slow.next);
        return root;
    }
```

建树比较方便的方法是递归，对于有序链表，高度平衡BST的根节点是其中点，然后该根节点的左子树的根节点，又是左半边的中点，该根节点的右子树的根节点，又是右半边的中点，以此往复，链表第一个节点，就是最左边左子树的根节点，而最左边左子树的左节点和右节点都是空。我们可以用start和end两个值来限定子树在链表中的位置，通过递归的方式，实际上可以实现顺序遍历链表然后建树的过程。不过java中，需要将链表当前遍历到节点作为全局变量，保证递归过程中链表也是顺序遍历的。

```java
public class Solution {

    ListNode curr;

    public TreeNode sortedListToBST(ListNode head) {
        curr = head;
        int len = 0;
        // 先计算出链表的长度
        while(head != null){
            head = head.next;
            len++;
        }
        // 开始建树
        return buildTree(0, len - 1);
    }

    //build以curr node开头，start~end长度的树返回，并且把curr挪到end+1点的位置
    private TreeNode buildTree(int start, int end){
        // 如果start>end，说明子树已经小到没有节点了，直接返回null
        if(start > end){
            return null;
        }
        // 找到中点
        int mid = start + (end - start) / 2;
        // 先递归的计算左子树
        TreeNode left = buildTree(start, mid - 1);
        // 然后建立根节点
        TreeNode root = new TreeNode(curr.val);
        // 链表顺序遍历
        curr = curr.next;
        // 最后计算右子树
        TreeNode right = buildTree(mid + 1, end);
        // 将三个节点连接起来
        root.left = left;
        root.right = right;
        return root;
    }
}
```

二刷

分治递归：类比Convert sorted array,想到要找到list的中点，要知道list中点必须要知道list的长度。所以可以传入长度和头节点来递归，每次递归通过长度一半遍历得到中间节点，然后根据中间节点分治左右子数

* 注意递归的base case:`if (head == null || len == 0) return null;`
* 注意根据长度求中点时 curr &lt; len / 2  可以想例子 比如长度是4时，可以取第2或者3的点，那么curr从0开始可以到2，然后跳出循环，所以curr &lt; len / 2

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

### 时间复杂度:O\(n\)

* 获取长度时候遍历一遍链表 O\(n\)
* 递归时候每个list节点访问一次 O\(n\)

一刷

分治的思想  
curr做根节点 慢慢往后挪

网上又看到一种自底向上的方法，算法复杂度为O\(N\)。先递归构建左子树，在构建左子树的同时不断移动链表的头指针，链表的头指针永远是对应当前子树位置的。一直到左叶子节点，左叶子节点对应的就是链表的第一个元素，生成左叶子节点之后移动链表当前指针

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



