# 走迷宫问题 DFS & BFS

```
               {{1, 5, 5, 5, 5, 0},
                {0, 5, 0, 5, 5, 0},
                {0, 5, 0, 0, 0, 0},
                {0, 5, 0, 0, 5, 0},
                {0, 0, 0, 0, 0, 9}};
                
判断能否从1走到9，能的话还要打印路径
```


### 关于打印路径


* DFS打印路径简单 只要不断记录加入的值，最后reverse一下就行了（reverse是因为深度优先找到结果值才会逐层返回）

* BFS 打印路径就烦一点，要有个map key存符合的点，value存他是从哪个点来的，根据map打印出来 在reverse一下


### DFS解法
```java
public class MazeBFSDFS {
    static int m;
    static int n;
    static List<String> path = new ArrayList<>();
    
    public static boolean canReach(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return false;
        m = matrix.length;
        n = matrix[0].length;
        
        boolean[][] visited = new boolean[m][n];
        return dfs(matrix, 0, 0, visited);
    }
    
    private static boolean dfs(int[][] matrix, int x, int y, boolean[][] visited) {
        if (matrix[x][y] == 9) {
            return true;
        }
        
        int[][] dict = {{-1,1,0,0},{0,0,-1,1}};
        visited[x][y] = true;
        for (int i = 0; i < 4; i++) {
            int newX = x + dict[0][i];
            int newY = y + dict[1][i];
            if (newX < 0 || newX >= m || newY < 0 || newY >= n) continue;
            if (matrix[newX][newY] == 5) continue;
            if (visited[newX][newY]) continue;
            if (dfs(matrix,newX, newY, visited)) {
                path.add(newX + " " + newY);
                return true;
            }
        }
        return false;
    }
    
    private static void printPath(){
        Collections.reverse(path);
        System.out.println(path);
    }
}

    public static void main(String[] args) {
        int[][] matrix = 
               {{1, 5, 5, 5, 5, 0},
                {0, 5, 0, 5, 5, 0},
                {0, 5, 0, 0, 0, 0},
                {0, 5, 0, 0, 5, 0},
                {0, 0, 0, 0, 0, 9}};
        System.out.println(canReach(matrix));
        
        printPath();
    }

```

