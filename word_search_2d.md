# Word Search (2D)
Given a 2D board and a word, find if the word exists in the grid.
* 先找到满足第一个字母的点，然后从这个点上下左右DFS
* 注意要记录访问过的点，return时候再变回来

优化方案
1. String变成char[]来处理
2. 不用visited数组，直接标记当前字母为"#"，最后返回时再标记回来


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