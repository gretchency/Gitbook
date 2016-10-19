# Detect Cycle In a directed graph

* 对一个起始点进行 递归调用的栈上的所有顶点进行标记，如果在 递归深入的过程中（非递归回退）遇到了已经在栈上的点，则说明有环。对所有未经过的顶点进行递归调用结束后，如果未发现有环，则说明图中无环。 

* 可以用两个HashSet,一个Visiting表示在栈上递归，一个Visited表示已经递归完这个节点，某一节点结束递归调用后将其从visiting中移除，并将其加入visited set.

```java


class Snap {
    List<Snap> next = new ArrayList<>();

    boolean hasCycle() {
        //visiting 记录在递归调用该点
        Set<Snap> visiting = new HashSet<>();
        //visited 表示已经递归调用完成的点
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
```

