# Path Sum II (树的dfs)
Given the below binary tree and sum = 22,
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```
return 
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

二刷（不用回溯）
* 每次操作前先new一个newPath,在newPath上操作

```java
public class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        List<Integer> path = new ArrayList<>();
        dfs(root, sum, res, path);
        return res;
    }
    
    private void dfs(TreeNode root, int sum, List<List<Integer>> res, List<Integer> path) {
        if (root == null) return;
        
        
        List<Integer> newPath = new ArrayList<>(path);
        sum -= root.val;
        newPath.add(root.val);
        if (root.left == null && root.right == null && sum == 0) {
            res.add(newPath);
            return;
        }
        
        dfs(root.left, sum, res, newPath);
        dfs(root.right, sum, res, newPath);
    }
}
```

* 经典树的DFS
  * 在 leaf node 符合要求加入结果集后backtracking，**因为后面的两个 dfs 都没有做，不走到底是不会回溯的**
  * 这点和常见的 subsets 和 permutations 不太一样，那两题中收尾直接 add 然后 return 就可以了，而回溯在 dfs 之后做
  * 处理完左右子树dfs后再backtracking,将用过的根节点删掉
 

```java
public class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        
        List<Integer> list = new ArrayList<>();
        dfs(root, sum, res, list);
        return res;
    }
    
    private void dfs(TreeNode root, int sum, List<List<Integer>> res, List<Integer> list) {
        if (root == null) return;
        
        if (root.left == null && root.right == null) {
            if (sum == root.val) {
                list.add(root.val);
                res.add(new ArrayList<>(list));
                //***注意这里加入结果集合要remove掉***
                list.remove(list.size() - 1);
            }
            return;
        }
        
        list.add(root.val);
        dfs(root.left, sum - root.val, res, list);
        dfs(root.right, sum - root.val, res, list);
        list.remove(list.size() - 1);
    }
}
```