# Add Two Numbers

```java
public class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        int carry = 0;
        while (l1 != null && l2 != null) {
            ListNode newNode = new ListNode((l1.val + l2.val + carry) % 10);
            carry = (l1.val + l2.val + carry) / 10;
            curr.next = newNode;
            curr = curr.next;
            l1 = l1.next;
            l2 = l2.next;
        }
        
        while (l1 != null) {
            ListNode newNode = new ListNode((l1.val + carry) % 10);
            carry = (l1.val + carry) / 10;
            curr.next = newNode;
            curr = curr.next;
            l1 = l1.next;
        }
        
        while (l2 != null) {
            ListNode newNode = new ListNode((l2.val + carry) % 10);
            carry = (l2.val + carry) / 10;
            curr.next = newNode;
            curr = curr.next;
            l2 = l2.next;
        }
        
        if (carry != 0) {
            curr.next = new ListNode(carry);
        }
        
        
        return dummy.next;
    }
}

```