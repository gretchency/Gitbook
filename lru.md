# LRU

```java
public class LRU {
    private class Node {
        private int key;
        private int value;
        private Node prev;
        private Node next;
        public Node(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }
    
    
    
    private int capacity;
    private Node head;
    private Node tail;
    private HashMap<Integer, Node> map;
    
    public LRU(int capacity) {
        this.capacity = capacity;
        head = new Node(0, 0);
        tail = new Node(0, 0);
        map = new HashMap<>();
        head.next = tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        if (!map.containsKey(key)) {
            return -1;
        }
        
        //Remove curr
        Node curr = map.get(key);
        curr.prev.next = curr.next;
        curr.next.prev = curr.prev;
        //Move to tail
        moveToTail(curr);
        
        return curr.value;        
    }
    
    public void set(int key, int value) {
        if(get(key) != -1) {
            map.get(key).value = value;
            return;
        }
        
        if (map.size() == capacity) {
            //remove head.next
            map.remove(head.next.key);
            head.next = head.next.next;
            head.next.prev = head;
        }
        Node node = new Node(key, value);
        map.put(key, node);
        moveToTail(node);
    }
    
    private void moveToTail(Node curr) {
        tail.prev.next = curr;
        curr.prev = tail.prev;
        curr.next = tail;
        tail.prev = curr;
    }

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        LRU lru = new LRU(3);
        lru.set(2, 2);
        lru.set(1, 1);
        lru.set(3, 3);
        System.out.println(lru.get(2));
        lru.set(5, 5);
        System.out.println(lru.get(2));
        System.out.println(lru.get(1));

    }

}
```