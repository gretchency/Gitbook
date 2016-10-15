# Reverse Linked List

```java
    public ListNode reverse(ListNode head) {
        // Reverse head.next to previous element
        ListNode prev = null;
        ListNode curr = head;
        while (curr != null) {
            ListNode temp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = temp;
        }
        return prev;
    }
```

翻转从m到n

二刷
* 先存一下mNode
* preM和prev相连
* mNode和curr相连

```java
        ListNode prev = null;
        //保存mNode
        ListNode mNode = preM.next;
        ListNode curr = mNode;
        //这是m <= n 找例子体会
        while (m <= n) {
            ListNode tmp = curr.next;
            curr.next =  prev;
            prev = curr;
            curr = tmp;
            m++;
        }
        
        preM.next = prev;
        mNode.next = curr;
        
        return dummy.next;
```


注意最后接上首尾！！

```java
public ListNode reverseBetween(ListNode head, int m , int n) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode preM = dummy;
        
        for (int i = 1; i < m; i++) {
            preM = preM.next;
        }
        
        ListNode prev = null;
        ListNode curr = preM.next;
        
        while (m <= n) {
            ListNode tmp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = tmp;
            m++;
        }
        
        //****注意先连接后面的再接前面的
        preM.next.next = curr;
        preM.next = prev;
        
        
        return dummy.next;

    }
```