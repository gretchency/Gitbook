# DFS


### DFS找环



白灰黑三种状态

白：unvisited  灰：visiting  黑:visited

一般处理方式：
* 从一个点出发dfs，看有无环（Course Schedule那题可能有多个连通区域，所以要对所有点dfs）
* 两个Set(visiting, visited)或者两个boolean数组存储访问状态。
* 如果撞上visiting就是有环，撞上visited就是通路。
* 把当前访问元素标记为visiting,dfs其连接节点。
* dfs完后将该节点visiting标记为fasle，将visited标记为true
