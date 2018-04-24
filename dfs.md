# DFS

DFS递归

想清楚三件事

* dfs\(\)函数做什么
  * 如subset, dfs\(res, list, nums\) 把所有以list里数开头的排列组合加入res
* dfs\(\)函数的终止条件
* 大问题如何转化为几个小问题，小问题如果转化为小小问题，循环往复

### DFS找环

环检测要点就是，找到一个还在遍历中的节点，同时在遍历的时候它如果再次被访问到了，则表示找到了环。而如果它被访问完了之后返回，则再次碰到它的时候就不是环了。

白灰黑三种状态

白：unvisited  灰：visiting  黑:visited

一般处理方式：

* 遍历所有点，分别从每个点出发dfs，看有无环（Course Schedule） 或者题目只要求看某一点出发是否有环（Detect Circle）
* 两个Set\(visiting, visited\)或者两个boolean数组或者一个HashMap存储访问状态。
* 如果撞上visiting就是有环，撞上visited就是通路。
* 把当前访问元素标记为visiting,dfs其连接节点。
* dfs完后将该节点visiting标记为fasle，将visited标记为true



