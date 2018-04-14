# BFS Binary Tree

最好的方法，使用一个Queue

每层poll的时候同时把每层的左右节点塞进queue

```java
    public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();

        //use a queue to store the level order and FIFO, so that can be added to the result by order
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        if (root == null) {
            return result;
        }
        queue.offer(root);

        while (!queue.isEmpty()) {
            ArrayList<Integer> level = new ArrayList<Integer>();
            //注意size要在循环外写，不然循环时size会变
            int size = queue.size();
            //把每一层的数依次加入level arraylist, 同时将每一个数的左右节点加入queue
            for (int i = 0; i < size; i++) {
                //System.out.println(queue.size());
                TreeNode head = queue.poll();
                level.add(head.val);

                //一定要判断是否null
                if (head.left != null) {
                    queue.offer(head.left);
                }

                if (head.right != null) {
                    queue.offer(head.right);
                }
            }
            //add to result by level
            result.add(level);
        }

        return result;
    }
```

reverse

[http://www.lintcode.com/en/problem/binary-tree-level-order-traversal-ii/](http://www.lintcode.com/en/problem/binary-tree-level-order-traversal-ii/)

```java
private ArrayList<ArrayList<Integer>> reverse(ArrayList<ArrayList<Integer>> result) {
        for (int i = 0, j = result.size() - 1; i < j; i++) {
            result.add(i, result.remove(j));
        }
        return result;
    }
```

DFS做BFS

maxLevel记录最大子树  
currLevel逐层遍历  
while里每次new一个level记录新level

```java
    //Deep-limited DFS

    public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();

        if (root == null) {
            return result;
        }

        int maxLevel = 0;
        while (true) {
            //**注意每次要在while循环里new level
            ArrayList<Integer> level = new ArrayList<Integer>();


            dfs(root, level, 0, maxLevel);
            //一旦level size为0，跳出循环
            if (level.size() == 0) {
                break;
            }
            result.add(level);
            maxLevel++;
        }

        return result;
    }

    private void dfs(TreeNode root, ArrayList<Integer> level, int currLevel, int maxLevel) {

        //curr>max就跳出
        if (root == null || currLevel > maxLevel) {
            return;
        }

        //curr == max就加入level
        if (currLevel == maxLevel) {
            level.add(root.val);
            return;
        }

        dfs(root.left, level, currLevel + 1, maxLevel);
        dfs(root.right,level, currLevel + 1, maxLevel);
    }
```



