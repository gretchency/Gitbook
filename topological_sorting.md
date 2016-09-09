# Topological Sorting

http://www.lintcode.com/en/problem/topological-sorting/#

Queue BFS

入度为0时加入队列

```java
public class Solution {
    /**
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */    
    public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        
        ArrayList<DirectedGraphNode> result = new ArrayList<DirectedGraphNode>();
        HashMap<DirectedGraphNode, Integer> map = new HashMap<DirectedGraphNode, Integer>();
        
        //统计所有点的入度
        for (DirectedGraphNode node: graph) {
            for (DirectedGraphNode neighbor: node.neighbors) {
                if (!map.containsKey(neighbor)) {
                    map.put(neighbor, 1);
                } else {
                    map.put(neighbor, map.get(neighbor) + 1);
                }
            }
        }
        
        //把入度为0的加入队列
        Queue<DirectedGraphNode> q = new LinkedList<DirectedGraphNode>();
        
        for (DirectedGraphNode node: graph) {
            if (!map.containsKey(node)) {
                q.offer(node);
                result.add(node);
            }
        }
        
        //把neighbors的入度减一 等于0的时候加入队列
        while (!q.isEmpty()) {
            DirectedGraphNode curr = q.poll();
            for (DirectedGraphNode neighbor : curr.neighbors) {
                map.put(neighbor, map.get(neighbor) - 1);
                if (map.get(neighbor) == 0) {
                    result.add(neighbor);
                    q.add(neighbor);
                }
            }
        }
        
        return result;

    }
}

```