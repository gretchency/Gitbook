# Merge k sorted LinkedList


http://www.lintcode.com/en/problem/merge-k-sorted-lists/#

First Solution: Priority Queue

O(nlog(k))

时间上，我们需要维护一个大小为k的最小值堆，每次维护复杂度O(logk)，由于一共有n个数据，每个数据都会加入最小值堆，故总体时间复杂度O(nlogk)。由于每个list至少有一个数据，故n一定大于等于k。相比于完全无序的n个数据排序(所需时间O(nlogn))，我们的算法将复杂度降至O(nlogk)。原因在于数据是部分有序的。事实上，在通常面试中，如果数据已经部分有序，我们理应能够实现时间复杂度优于O(nlogn)的算法。

空间上，我们需要大小为k的最小值堆。同时，在不允许破坏原有链表的情况下，我们需要额外O(n)的空间构建新链表，故总体空间复杂度O(n+k)。如果可以直接修改原有数据的next指针，则总体空间复杂度即为O(k)。至于是否能够破坏原始数据，需要与面试官进行沟通。

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

Merge sort

O(nlog(n))

```java
    public ListNode mergeKLists(List<ListNode> lists) {
        if (lists == null || lists.size() == 0) {
            return null;
        }
        
        return mergeSort(lists, 0, lists.size() - 1);
    }
    
    public ListNode mergeSort(List<ListNode> lists, int start, int end) {
        //注意base case
        if (start == end) {
            return lists.get(start);
        }
        
        int mid = start + (end - start) / 2;
        
        ListNode left = mergeSort(lists, start, mid);
        ListNode right = mergeSort(lists, mid + 1, end);
        
        return merge(left, right);
        
    }
    
    public ListNode merge(ListNode l1, ListNode l2) {
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