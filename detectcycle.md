# DetectCycle

分析： [link](https://gretchency.gitbooks.io/leetcode/content/detect_cycle_in_a_directed_graph.html)
```java
//经典有向图的环查找 dfs

public class DetectCircle {
    public static void main(String[] args) {
        Snap s1 = new Snap(), s2 = new Snap(), s3 = new Snap(), s4 = new Snap(), s5 = new Snap(), s6 = new Snap();
        s1.next.add(s5);
        s1.next.add(s2);
        s2.next.add(s3);
        s2.next.add(s5);
        s5.next.add(s4);
        s5.next.add(s6);

        System.out.println(s1.hasCycle());
    }
}

class Snap {
    List<Snap> next = new ArrayList<>();;

    boolean hasCycle() {
        //visiting 记录前检查哪个点
        Set<Snap> visiting = new HashSet<>();
        //visited 表示已经检查过的点
        Set<Snap> visited = new HashSet<>();
        return dfs(this, visiting, visited);
    }

    boolean dfs(Snap snap, Set<Snap> visiting, Set<Snap> visited) {
        if (visiting.contains(snap)) return true;
        if (visited.contains(snap)) return false;
        
        visiting.add(snap);
        
        for (Snap neighbor: snap.next) {
            if (dfs(neighbor, visiting, visited)) {
                return true;
            }
        }
        visiting.remove(snap);
        visited.add(snap);
        
        return false;
    }
}
```