# Rotate List(快慢指针）

http://www.lintcode.com/en/problem/rotate-list/#

![](Screen Shot 2016-09-01 at 3.43.20 PM.png)
快慢指针 快指针先走k % length步，慢指针开始走， 最后把该连的连， 该断的断

```java
public class Solution {
    /**
     * @param head: the List
     * @param k: rotate to the right k places
     * @return: the list after rotation
     */
     
    private int getLength(ListNode head) {
        int length = 0;
        while (head != null) {
            length++;
            head = head.next;
        }
        return length;
    }
    
    
    public ListNode rotateRight(ListNode head, int k) {
        
        if (head == null || head.next == null) {
            return head;
        }
        
        int length = getLength(head);
        
        int n = k % length;
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        ListNode tail = dummy;
        
        //head先走n步
        for (int i = 0; i < n; i++) {
            head = head.next;
        }
        
        //head和tail一起走
        while (head.next != null) {
            head = head.next;
            tail = tail.next;
        }
        
        //中间接上
        head.next = dummy.next;
        
        //作为头
        dummy.next = tail.next;
        
        //断开连接
        tail.next = null;
        
        return dummy.next;
    }
    
}
```