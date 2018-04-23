# N-Queen

经典DFS

* 大体思想就是在每一行放一粒棋子，然后dfs验证可行性
* 分为dfs,验证可行，画棋盘 三个主要函数
* 只需要一个int array存放col位置，其index就是row位置
* 对角线用`Math.abs`

Ref: https://blog.csdn.net/zhang245754954/article/details/52612784

![](/assets/import.png)

* **N-Queen II 注意**：不能直接把int value放里面传. 因为java函数的参数如果是int的话传的是值，所以每个sum都不一样。有三种解决方法，一种是函数返回int，也就是sum；第二种是用全局变量（不推荐）；第三种是用一个类的对象来记录sum，因为参数如果是对象的话传的是引用。

```java
public class Solution {
    /*
     * @param n: The number of queens
     * @return: All distinct solutions
     */
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> res = new ArrayList<>();

        if (n <= 0) return res;
        //存放棋子在每一行对应列的index
        List<Integer> colIndex = new ArrayList<>();
        dfs(res, colIndex, n);

        return res;
    }

    //return all the results that uses the current colIndex list
    private void dfs(List<List<String>> res, List<Integer> colIndex, int n) {
        if (colIndex.size() == n) {
            res.add(drawMap(colIndex, n));
            return;
        }

        for (int i = 0; i < n; i++) {
            int newCol = i;
            if (isValid(newCol, colIndex)) {
                colIndex.add(newCol);
                dfs(res, colIndex, n);
                colIndex.remove(colIndex.size() - 1);
            }
        }
    }

    //如果列数一样不行，都在对角线也不行
    private boolean isValid(int newCol, List<Integer> colIndex) {
        int oldSize = colIndex.size();
        int newRow = oldSize;
        for (int i = 0; i < oldSize; i++) {
            if (colIndex.get(i) == newCol) return false;
            //如果两棋子(a,b) (c,d)在对角线上，|a-c| = |b - d|
            if (Math.abs(newCol - colIndex.get(i)) == Math.abs(newRow - i)) return false;
        }

        return true;
    }

    private List<String> drawMap(List<Integer> colIndex, int n) {
        List<String> res = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            StringBuilder sb = new StringBuilder();
            for (int j = 0; j < n; j++) {
                if (colIndex.get(i) == j) {
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



