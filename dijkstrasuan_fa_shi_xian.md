# Dijkstra算法实现

邻接矩阵建图

* dist[]数组存放每个点的最短距离
* 先根据第一个点到所有点的距离初始化dist
* 然后标记第一个点visited
* 找没有visited里最小距离的点，标记该点为visited.根据该点找通过该点转接比原先dict[]数组记录距离小的点，更新dict.
```java
dist[minIndex] + graph[minIndex][k] < dist[k]```
* 周而复始，，知道所有点都visited了


```java
package Lattice;

import java.util.LinkedList;
import java.util.Queue;

public class EasyDijkstra {
    private static final int INF = Integer.MAX_VALUE;
    
    public static int[] Calculate(int[][] graph) {
        //初始化dist[]数组里的距离
        int n = graph.length;
        int[] dist = new int[n];
        String[] path = new String[n];
        for (int i = 0; i < n; i++) {
            path[i] = new String("0 -->" + i);
        }
            
        
        //一开始就是入口到各个点的距离
        for (int i = 0; i < n; i++) {
            dist[i] = graph[0][i];
        }
        
        //入口访问过了
        boolean[] visited = new boolean[n];
        visited[0] = true;
        
        
        //遍历知道所有点都visited了 因为0点默认visited,所以n-1
        int unvisited = n - 1;
        //这里替代队列的作用
        while(unvisited > 0) {
            int min = Integer.MAX_VALUE;
            int minIndex = -1;
            for (int j = 0; j < n; j++) {
                //找到当前最小的没被访问的点
                if (!visited[j] && dist[j] < min) {
                    min = dist[j];
                    minIndex = j;
                }
            }
            //该点over
            visited[minIndex] = true;
            
            for (int k = 0; k < n; k++) {
                //判断是否从minIndex到得了k
                if (graph[minIndex][k] < Integer.MAX_VALUE) {
                    //松弛效果比原来的值小就更新
                    if (dist[minIndex] + graph[minIndex][k] < dist[k]) {
                        dist[k] = dist[minIndex] + graph[minIndex][k];
                        path[k] = path[minIndex] + "-->" + k;
                    }
                }
            }
            unvisited--;
        }
        
        for (int i = 0; i < n; i++) {
            System.out.println("从" + 0 + "到" + i + "的最短路径：" + path[i]);
        }
        
        return dist;
    }
    
    public static void main(String[] args) {
        int[][] graph = new int[][] { 
            { 0, 2, INF, 1, INF, INF, INF }, 
            { INF, 0, INF, 3, 10, INF, INF },
            { 4, INF, 0, INF, INF, 5, INF }, 
            { INF, INF, 2, 0, 2, 8, 4 }, 
            { INF, INF, INF, INF, 0, INF, 6 },
            { INF, INF, INF, INF, INF, 0, INF }, 
            { INF, INF, INF, INF, INF, 1, 0 } };
 
        int[] dis = Calculate(graph);
 
        for (int i = 0; i < dis.length; i++)
            System.out.println(dis[i]);
    }
}

```