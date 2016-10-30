# Binary Tree 整合

Maximum depth of a Binary Tree

Binary Tree Preorder Travesal

***Binary Tree Maximum Path Sum*** [leet](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
* 要使路径和最大，则必然要使左子树和右子树中的路径长度都取最大。
* 全局变量maxValue记录全局最大和
* 递归函数返回root的子树到root节点(含)路径长度的最大值
* 在求局部最大值的时候，需要当前节点的值加上左右子树中的最大值,巧妙利用0。若子树为负，则取值0
* 不断更新maxValue

Binary Tree Maximum Path Sum II
* 注意最后如果小于0就不要
* ```return root.val + Math.max(0, Math.max(left, right));```



inorder successor in binary search tree
* inorder travesal 在traversal的过程中有一个Boolean 一开始false 后面相等时变true,下一个节点就是successor

Validate Binary Search Tree
* 递归要用long
* 非递归就是inorder traversal一遍看是否升序

Balanced Binary Tree
* 求出左右子树的高度，相减绝对值>1就不平衡，左右递归求证

**Lowest Common Ancestor**
1. BST
* 根据bst性质只要root!=null就往下找，遇到p，q分列root左右子树的时候就return root.
2. Binary Tree
* 左右分治，左右都不为空就在root,左边不空右边空返回左边，反之返回右边。

**Binary Tree Level Order Traversal**
* 按层遍历 遍历前先确定每一层的size for循环将该层节点加入list

**Binary Search Tree Iterator**
* Binary Tree的非递归中序遍历分开来写
* 实例变量curr记录节点位置

---

[**Largest BST SubTree**](https://gretchency.gitbooks.io/leetcode/content/largest_bst_subtree.html)

非常好的一道题目，问题包含了三个block,求最大BST节点个数，求子树节点个数，和判断Valid BST.

递归求解，分为三种状态
1. 递归到了叶子节点，返回1
2. 遇到了valid bst,返回该tree节点个数（递归求解）
3. 本身不是valid bst,返回左右子树中最大的valid bst节点个数

[House Robber III](https://gretchency.gitbooks.io/leetcode/content/house_robber_iii.html)

* 还是类比House RobberI II,分成偷当前节点和不偷当前节点两种情况，然后比较哪个大。
  * 需要维护两个元素的res数组，分别是有root的最大值和没root的最大值
  * dfs分治求left,right,和root节点比较求解出最大情况

[Unique BST](https://gretchency.gitbooks.io/leetcode/content/unique_bst_dp.html)
* 选取一个结点为根，就把结点切成左右子树，以这个结点为根的可行二叉树数量就是左右子树可行二叉树数量的乘积
* 总的数量是将以所有结点为根的可行结果累加起来