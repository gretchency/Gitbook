# Clone Graph

http://www.lintcode.com/en/problem/clone-graph/#


BFS: ArrayList + HashMap

Ralated: Copy List with Random Pointer

```java
/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    /**
     * @param node: A undirected graph node
     * @return: A undirected graph node
     */
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        ArrayList<UndirectedGraphNode> nodes = new ArrayList<UndirectedGraphNode>();
        HashMap<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap<UndirectedGraphNode, UndirectedGraphNode>();
        
        if (node == null) {
            return null;
        }
        
        //Clone Nodes
        
        nodes.add(node);
        //拷贝方法是用用HashMap，key存原始值，value存copy的值
        map.put(node, new UndirectedGraphNode(node.label));
        
        int start = 0;
        
        //用start指针把每个点的neighbor都加进来
        //同时用map判断避免重复加
        while (start < nodes.size()) {
            UndirectedGraphNode head = nodes.get(start);
            for (int i = 0; i < head.neighbors.size(); i++) {
                UndirectedGraphNode neighbor = head.neighbors.get(i);
                if (!map.containsKey(neighbor)) {
                    nodes.add(neighbor);
                    map.put(neighbor, new UndirectedGraphNode(neighbor.label));
                }
            }
            start++;
        }
        
        
        //Clone Neighbors
        
        //两层循环把neighbors加上
        for (int i = 0; i < nodes.size(); i++) {
            UndirectedGraphNode newNode = map.get(nodes.get(i));
            for (int j = 0; j < nodes.get(i).neighbors.size(); j++) {
                UndirectedGraphNode newNeighbor = map.get(nodes.get(i).neighbors.get(j));
                newNode.neighbors.add(newNeighbor);
            }
        }
        
        return map.get(node);
    }
}
```