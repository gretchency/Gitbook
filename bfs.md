# BFS


BFS套路

* HashMap记录最短距离和去重
```java
public class BFS {
    private static void bfs(HashMap<Character, LinkedList<Character>> graph,char start) {
        if (graph == null || graph.size() == 0) return;

        Map<Character, Integer> dist = new HashMap<>();
        Queue<Character> q = new LinkedList<>();

        q.offer(start);
        dist.put(start, 0);

        while (!q.isEmpty()) {
            char curr = q.poll();
            //System.out.println(curr + "shortest distance is " + dist.get(curr));
            int newD = dist.get(curr) + 1;
            for (Character next: graph.get(curr)) {
                if (dist.containsKey(next)) continue;
                map.put(next, newD);
                
                q.offer(next);
            }
        } 
    }
}
```