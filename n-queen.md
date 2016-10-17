# N-Queen

经典DFS
* 大体思想就是在每一行放一粒棋子，然后dfs验证可行性
* 分为dfs,验证可行，画棋盘 三个主要函数
* 只需要一个int array存放col位置，其index就是row位置
* 对角线用```Math.abs```

* **N-Queen II 注意**：不能直接把int value放里面传. 因为java函数的参数如果是int的话传的是值，所以每个sum都不一样。有三种解决方法，一种是函数返回int，也就是sum；第二种是用全局变量（不推荐）；第三种是用一个类的对象来记录sum，因为参数如果是对象的话传的是引用。

```java
public class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> res = new ArrayList<>();
        
        if (n < 0) return res;
        //index为row, 值为col
        List<Integer> rows = new ArrayList<>();
        
        dfs(res, rows, n);
        
        return res;
    }
    
    private void dfs(List<List<String>> res, List<Integer> rows, int n) {
        if (rows.size() == n) {
            res.add(drapMap(rows));
            return;
        }
        
        //找每一层放在那一列， i为列数
        for (int i = 0; i < n; i++) {
            if(isValid(rows, i)) {
                rows.add(i);
                dfs(res, rows, n);
                //回溯
                rows.remove(rows.size() - 1);
            }
        }
    }
    
    private boolean isValid(List<Integer> rows, int newCol) {
        int oldSize = rows.size();
        int newRow = oldSize;
        for (int i = 0; i < oldSize; i++) {
            int oldCol = rows.get(i);
            //不能在同一列
            if (oldCol == newCol) return false;
            //不能在对角线
            if (Math.abs(i - newRow) == Math.abs(oldCol - newCol)) return false;
        }
        
        return true;
    }
    
    private List<String> drapMap(List<Integer> rows) {
        List<String> res = new ArrayList<>();
        for (int i = 0; i < rows.size(); i++) {
            //每一行用一个sb构造
            StringBuilder sb = new StringBuilder();
            for (int j = 0; j < rows.size(); j++) {
                if (rows.get(i) == j) {
                    sb.append("Q");
                } else {
                    sb.append(".");
                }
            }
            res.add(sb.toString());
        }
        return res;
    }
}
```

