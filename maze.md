# Maze
```
走迷宫问题。给了一个矩阵，"1"代表起点，位于左上角；"9"代表重点，位于右下角；"0"代表通路，"5"代表墙。. 
矩阵长得是这样

		[
		  [1, 5, 5, 5, 5, 0],
		  [0, 5, 0, 5, 5, 0], 
		  [0, 5, 0, 0, 0, 0],
		  [0, 5, 0, 0, 5, 0],
		  [0, 0, 0, 5, 0, 9]
		]
设计一个算法，看看这个迷宫能不能从起点走到重点。
```



```java
public class Maze {
    public static void main(String[] args) {
        int[][] matrix = 
               {{1, 5, 5, 5, 5, 0},
                {0, 5, 0, 5, 5, 0},
                {0, 5, 0, 0, 0, 0},
                {0, 5, 0, 0, 5, 0},
                {0, 0, 0, 5, 5, 9}};
        System.out.println(canReach(matrix));
        
        printPath();
    }

    private static int m;
    private static int n;
    private static List<String> path = new ArrayList<>();
    
    public static boolean canReach(int[][] matrix) {
        m = matrix.length - 1;
        n = matrix[0].length - 1;
        boolean[][] visited = new boolean[matrix.length][matrix[0].length];
        return search(matrix, visited, 0, 0);
    }
    
    private static void printPath() {
        Collections.reverse(path);
        System.out.println(path);
    }
    
    //dx dy用来向四个方向走
    private static int[] dx = {-1, 1, 0, 0};
    private static int[] dy = {0, 0, -1, 1};
    
    private static boolean search (int[][] matrix, boolean[][] visited, int x, int y) {
        
        
        if (visited[x][y]) return false;
        
        if (matrix[x][y] == 9) return true;
        
        visited[x][y] = true;
        for (int i = 0; i < dx.length; i++) {
            int a = x + dx[i];
            int b = y + dy[i];
            if (a < 0 || a > m || b < 0 || b > n) continue;
            if (matrix[a][b] == 5) continue;
            
            if (search(matrix, visited, a, b)) {
                path.add(a + " " + b);
                return true;

            }
            
        }
        
        
        return false;
    }

    
}
```