# Rehashing

http://www.lintcode.com/en/problem/rehashing/\#

```java
public class Solution {
    /**
     * @param hashTable: A list of The first node of linked list
     * @return: A list of The first node of linked list which have twice size
     */    
    public ListNode[] rehashing(ListNode[] hashTable) {
        // write your code here
        if (hashTable == null || hashTable.length == 0) return null;
        
        int oldSize = hashTable.length;
        int newSize = 2 * oldSize;
        
        ListNode[] oldArray = hashTable;
        hashTable = new ListNode[newSize];
        
        for (ListNode node: oldArray) {
            if (node != null) {
                ListNode curr = node;
                while (curr != null) {
                    insert(curr.val, hashTable);
                    curr = curr.next;
                }
            }
        }
        
        return hashTable;
    }
    
    private void insert(int key, ListNode[] hashTable) {
        // if key is negative value
        int hashVal = (key % hashTable.length + hashTable.length) % hashTable.length;
        
        if (hashTable[hashVal] == null) {
            hashTable[hashVal] = new ListNode(key);
            return;
        }
        
        ListNode head = hashTable[hashVal];
        ListNode curr = head;
        while (curr.next != null) {
            curr = curr.next;
        }
        curr.next = new ListNode(key);
    }
    
};
```



