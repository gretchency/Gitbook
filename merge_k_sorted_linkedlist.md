# Merge k sorted LinkedList


http://www.lintcode.com/en/problem/merge-k-sorted-lists/#

First Solution: Priority Queue

O(nlog(k))

```java
private Comparator<ListNode> ListNodeComparator = new Comparator<ListNode>() {
        public int compare(ListNode left, ListNode right) {
            // if (left == null || right == null) {
            //     return -1;
            // }
            
            return left.val - right.val;
        }
    };
    
    public ListNode mergeKLists(List<ListNode> lists) {
        if (lists == null || lists.size() == 0) {
            return null;
        }
        
        
        //要用comparator 不然没法比
        PriorityQueue<ListNode> pq = new PriorityQueue<ListNode>(lists.size(), ListNodeComparator);
        
        //先把所有lists的头比较
        for (int i = 0; i < lists.size(); i++) {
            if (lists.get(i) != null) {
                pq.offer(lists.get(i));
            }
        }
        
        ListNode dummy = new ListNode(0);
        
        //用curr处理 dummy留着
        ListNode curr = dummy;
        
        while(!pq.isEmpty()) {
            ListNode head = pq.poll();
            curr.next = head;
            curr = head;
            
            //如果head后面还有node, 加入pq
            if (head.next != null) {
                pq.offer(head.next);
            }
        }
        
        return dummy.next;
        
    }
```

Related:

 Merge Two Sorted Lists
 
 ```java
 public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                curr.next = l1;
                l1 = l1.next;
            } else {
                curr.next = l2;
                l2 = l2.next;
            }
            
            curr = curr.next;

        }
        
        if (l1 != null) {
            curr.next = l1;
        } else {
            curr.next = l2;
        }
        
        return dummy.next;
    }
 ```