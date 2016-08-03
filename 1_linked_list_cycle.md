# 1. Linked List Cycle

```java
    public boolean hasCycle(ListNode head) {  
        if (head == null || head.next == null) {
            return false;
        }
        
        // fast and slow listnodes
        ListNode fast = head;
        ListNode slow = head;
        
        //Determine if fast can move two steps
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (fast == slow) {
                return true;
            }
        }
        return false;
    }
```
