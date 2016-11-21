# Word Search (2D)
Given a 2D board and a word, find if the word exists in the grid.
* 先找到满足第一个字母的点，然后从这个点上下左右DFS
* 注意要记录访问过的点，return时候再变回来

优化方案
1. String变成char[]来处理
2. 不用visited数组，直接标记当前字母为"#"，最后返回时再标记回来


### 时间复杂度：

从一个字符矩阵中搜索某个字符串是否存在，可以向四个方向延伸。那么dfs和bfs的时间复杂度是指数级别的，大概是4的字符串长度次方，因为每次都可能走四个方向

Time : m*n*4^(k-1). 也就是m*n*4^k

二刷
* 注意要在前面判断i和j是否valid，而不是在for循环里面判断，否则只有一个元素的情况过不了。

```java
public class Solution {
    private int[][] dict = {{-1,1,0,0},{0,0,-1,1}};
    public boolean exist(char[][] board, String word) {
        if (word == null || word.length() == 0) return true;
        
        int m = board.length;
        int n = board[0].length;
        char[] chars = word.toCharArray();
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == chars[0]) {
                    if(dfs(board, i, j, chars, 0)) return true;
                }
            }
        }
        
        return false;
    }
    
    
    
    private boolean dfs(char[][] board, int i, int j, char[] word, int start) {
        if (start == word.length) return true;
        
        //****在前面判断****
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != word[start]) return false;
        char c = board[i][j];
        board[i][j] = '#';
        for (int k = 0; k < dict[0].length; k++) {
            int newI = i + dict[0][k];
            int newJ = j + dict[1][k];
            
            
            if (dfs(board, newI, newJ, word, start + 1)) {
                return true;
            }
        }
        board[i][j] = c;
        return false;
    }
}
```

```java
public class Solution {
    public boolean exist(char[][] board, String word) {
        if (word == null || word.length() == 0) return true;
        
        int m = board.length;
        int n = board[0].length;
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                //先找到1个起点
                if (board[i][j] == word.charAt(0)) {
                    //不能直接return，还有别的起点
                    if(dfs(board, i, j, word, 0)) return true;
                }
            }
        }
        
        return false;
    }
    
    
    private boolean dfs(char[][] board, int i, int j, String word, int start) {
        if (start == word.length()) return true;
        
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != word.charAt(start)) return false;
        
        //相当于visited,省下mn空间，记录下原值
        char c = board[i][j];
        board[i][j] = '#';
        
        boolean res = dfs(board, i + 1, j, word, start + 1) || 
                      dfs(board, i - 1, j, word, start + 1) ||
                      dfs(board, i, j + 1, word, start + 1) ||
                      dfs(board, i, j - 1, word, start + 1);
        //变回原值
        board[i][j] = c;
        
        return res;
    }
}
```