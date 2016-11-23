# Number Of Islands
DFS BFS均可

将用过的1标记为2去重，最后再把2变为1

时间：O(mn)
```java
public class Solution {
    
    private int m, n;
    public int numIslands(char[][] grid) {
        m = grid.length;
        if (m == 0) return 0;
        n = grid[0].length;
        
        if (n == 0) return 0;
        int count = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] != '1') continue;
                count++;
                dfs(grid, i, j);
            }
        }
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '2') {
                    grid[i][j] = '1';
                }
            }
        }
        
        return count;
    }
    
    private int[][] dict = {{-1,1,0,0},{0,0,-1,1}};
    private void dfs(char[][] grid, int i, int j) {
        if (i < 0 || i >= m || j < 0 || j >= n) return;
        if (grid[i][j] != '1') return;
        grid[i][j] = '2';
        for (int k = 0; k < 4; k++) {
            int newI = i + dict[0][k];
            int newJ = j + dict[1][k];
            dfs(grid, newI, newJ);
        }
            
    }
}
```


## Follow Up:


## Largest Island

```
2D matrix with ‘0’, ‘X’，return the max area connected (max area of island)
```

一样的思路，把用过的标记为'#'，最后再标记回来,并用max变量不断更新最大岛屿

```java
public class MaxAreaConnected {
    private static int m;
    private static int n;
    private static int[][] dict = {{-1,1,0,0},{0,0,-1,1}};
    public static int getArea(char[][] map) {
        if (map == null || map.length == 0 || map[0] == null || map[0].length == 0) return 0;
        int max = 0;
        m = map.length;
        n = map[0].length;
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (map[i][j] == 'O') {
                    int count = dfs(i,j,map, 0);
                    max = Math.max(max, count);
                }
            }
        }
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (map[i][j] == '#') {
                    map[i][j] = 'O';
                }
            }
        }
        
        return max;
    }
    
    private static int dfs(int i, int j, char[][] map, int count) {
        if (i < 0 || i >= m || j < 0 || j >= n || map[i][j] != 'O') {
            return count;
        }
        
        map[i][j] = '#';
        count++;
        for (int k = 0; k < 4; k++) {
            int newI = i + dict[0][k];
            int newJ = j + dict[1][k];
            count = dfs(newI, newJ, map, count);
        }
        
        return count;
    }
}
```


