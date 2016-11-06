# Binary Tree Vertical Order Treversal

* 两个Queue,一个装TreeNode,一个装它所在的col
* 用map记录每一列的TreeNode val
* 同时维护min max col，从而最后输出结果

```java
public class Solution {
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        
        Queue<TreeNode> q = new LinkedList<>();
        Queue<Integer> col = new LinkedList<>();
        Map<Integer, List<Integer>> map = new HashMap<>();
        q.offer(root);
        col.offer(0);
        
        int min = 0;
        int max = 0;
        while (!q.isEmpty()) {
            TreeNode curr = q.poll();
            int currCol = col.poll();
            
            if (map.containsKey(currCol)) {
                map.get(currCol).add(curr.val);
            } else {
                List<Integer> list = new ArrayList<>();
                list.add(curr.val);
                map.put(currCol, list);
            }
            
            if(curr.left != null) {
                q.offer(curr.left);
                col.offer(currCol - 1);
                min = Math.min(min, currCol - 1);
            }
            
            if(curr.right != null) {
                q.offer(curr.right);
                col.offer(currCol + 1);
                max = Math.max(max, currCol + 1);
            }
        }
        
        for (int i = min; i <= max; i++) {
            res.add(map.get(i));
        }
        
        return res;
    }
}

```