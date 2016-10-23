# Binary Tree 整合

Maximum depth of a Binary Tree

Binary Tree Preorder Travesal

***Binary Tree Maximum Path Sum*** [leet](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
* 全局变量maxValue记录全局最大和
* 递归函数返回子树中经过当前节点的局部最大和
* 在求局部最大值的时候，需要当前节点的值加上左右子树中的最大值
* 巧妙利用0。若子树为负，则取值0

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

**Largest BST SubTree**

非常好的一道题目，问题包含了三个block,求最大BST节点个数，求子树节点个数，和判断Valid BST.

递归求解，分为三种状态
1. 递归到了叶子节点，返回1
2. 遇到了valid bst,返回该tree节点个数（递归求解）
3. 本身不是valid bst,返回左右子树中最大的valid bst节点个数