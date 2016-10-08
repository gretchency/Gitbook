# Topological Sorting

http://www.lintcode.com/en/problem/topological-sorting/#

二刷
* 需要理解的是入度的概念，前面的相关入度全部完成后，才能走后面的入度


Queue BFS

以 V 表示顶点数，E 表示有向图中边的条数。

首先获得节点的入度数，时间复杂度为 O(V+E), 使用了哈希表存储，空间复杂度为 O(V). 遍历图求得入度为0的节点，时间复杂度为 O(V). 仅在入度为0时调用 DFS，故时间复杂度为 O(V+E).

需要注意的是这里的 DFS 不是纯 DFS，使用了 BFS 的思想进行了优化，否则一个节点将被遍历多次，时间复杂度可能恶化为指数级别。

综上，时间复杂度近似为 O(V+E), 空间复杂度为 O(V).

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