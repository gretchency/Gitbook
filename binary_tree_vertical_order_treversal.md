# Binary Tree Vertical Order Treversal

* 两个Queue,一个装TreeNode,一个装它所在的col
* 用map记录每一列的TreeNode val
* 同时维护min max col，从而最后输出结果