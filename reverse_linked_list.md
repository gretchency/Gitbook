# Reverse Linked List

```java
    public ListNode reverse(ListNode head) {
        // Reverse head.next to previous element
        ListNode prev = null;
        while (head != null) {
            ListNode temp = head.next;
            head.next = prev;
            prev = head;
            head = temp;
        }
        return prev;
    }
```

翻转从m到n


注意最后接上首尾！！

```java
   public ListNode reverseBetween(ListNode head, int m , int n) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        
        //注意i从1开始
        for(int i = 1; i < m; i++) {
            //一定要判断head.next 是否为null
            if (head.next == null) {
                return null;
            }
            head = head.next;
        }
        
        
        ListNode prev = head;
        //mNode is the tail of the reversed linked list
        ListNode mNode = head.next;
        //nNode is the head of the reversed linked list
        ListNode nNode = mNode;
        ListNode postnNode = mNode.next;
        
        
        for(int i = m; i < n; i++) {
            if (postnNode == null) {
                return null;
            }
            //把nNode作为prev，reverse linked list 
            ListNode temp = postnNode.next;
            postnNode.next = nNode;
            nNode = postnNode;
            postnNode = temp;
        }
        
        //最后把首尾接上
        prev.next = nNode;
        mNode.next = postnNode;
        
        return dummy.next;
    }
```