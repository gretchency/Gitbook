# LRU Cache

http://www.lintcode.com/en/problem/lru-cache/

分析： 序列： 从中间删除一个数 再append到尾巴上 ==> lineked list
HashMap + LinkedList

二刷
* 根据题意要存放node,每个node都有key, val，所以根据此建立node class
* 由于node删除操作要知道前后的点，所以用doubly linked list
* 注意capacity满了以后 不仅要删除第一个node 还要删除map的对应node!
* set时候如果Cache里已经有key，要更新value!

```java
public class LRUCache {
    //可以无视outer class独立存在
    private static class Node {
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
    private Node head = new Node(0, 0);
    private Node tail = new Node(0, 0);
    private HashMap<Integer, Node> map = new HashMap<Integer, Node>();
    
    public LRUCache(int capacity) {
        this.capacity = capacity;
        //Construct里接好head和tail
        head.next = tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        //如果get不到 return -1
        if (!map.containsKey(key)) {
            return -1;
        }
        
        //删掉当前位置
        Node curr = map.get(key);
        curr.prev.next = curr.next;
        curr.next.prev = curr.prev;
        
        //move to tail
        moveToTail(curr);
        
        return curr.value;
    }
    
    public void set(int key, int value) {
        //如果已经在cache了 更新value
        if (get(key) != -1) {
            map.get(key).value = value;
            return;
        }
        
        //不在cache, 先判断cache满了没
        if (map.size() == capacity) {
            //***注意先把map里的key删了
            map.remove(head.next.key);
            //把head.next删了
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
}
```