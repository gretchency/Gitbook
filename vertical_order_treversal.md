# Vertical Order Treversal

```java
//多加一个col queue BFS,左子树就col - 1, 右子树就col + 1, 用map记录相同col的node值，最后遍历map
public class verticalOrderTre {
    public static class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        public TreeNode(int val) {
            this.val = val;
        }
    }
    
    public static List<List<Integer>> vertical(TreeNode root) {
        if (root == null) return null;
        
        List<List<Integer>> res = new ArrayList<>();
        Map<Integer, List<Integer>> map = new HashMap<>();
        Queue<TreeNode> nodes = new LinkedList<>();
        Queue<Integer> cols = new LinkedList<>();
        nodes.offer(root);
        cols.offer(0);
        
        //注意min max 记录最小最大位置
        int min = 0;
        int max = 0;
        while (!nodes.isEmpty()) {
            TreeNode node = nodes.poll();
            int col = cols.poll();
            if (map.containsKey(col)) {
                map.get(col).add(node.val);
            } else {
                map.put(col, new ArrayList<Integer>(Arrays.asList(node.val)));
            }
            
            if (node.left != null) {
                nodes.offer(node.left);
                cols.offer(col - 1);
                min = Math.min(min, col - 1);
            }
            
            if (node.right != null) {
                nodes.offer(node.right);
                cols.offer(col + 1);
                max = Math.max(max, col + 1);
            }            
        }
        
        for (int i = min; i <= max; i++) {
            res.add(map.get(i));
        }
        
        return res;
    }
    
    public static void main(String[] args) {
        // TODO Auto-generated method stub
        TreeNode root = new TreeNode(5);
        TreeNode lc = new TreeNode(4);
        TreeNode rc = new TreeNode(3);
        root.left = lc;
        root.right = rc;
        
        System.out.println(vertical(root));
    }
    
    
}
```