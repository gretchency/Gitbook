# Sort List

http://www.lintcode.com/en/problem/sort-list/

Merge Sort的思想

```java
public class Solution {
    /**
     * @param head: The head of linked list.
     * @return: You should return the head of the sorted linked list,
                    using constant space complexity.
     */
    
    public ListNode findMiddle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        //注意还要判断fast.next!=null
        while (fast.next != null && fast.next.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
    
    public ListNode merge(ListNode head1, ListNode head2) {
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        while (head1 != null && head2 != null) {
            if (head1.val < head2.val) {
                curr.next = head1;
                head1 = head1.next;
            } else {
                curr.next = head2;
                head2 = head2.next;
            }
            //curr往后走一格
            curr = curr.next;
        }
        //如果head1没走完,都是head1
        if (head1 != null) {
            curr.next = head1;
        } else {
            //head2没走完，都是head2
            curr.next = head2;
        }
        return dummy.next;
    }
    
    public ListNode sortList(ListNode head) {  
        //判断head
        if (head == null || head.next == null) {
            return head;
        }
        ListNode mid = findMiddle(head);
        //先sort右边 再断开右边
        ListNode right = sortList(mid.next);
        
        //*****注意这里要断开mid.next
        mid.next = null;
        ListNode left = sortList(head);
        return merge(left, right);
    }
    
    

}
```