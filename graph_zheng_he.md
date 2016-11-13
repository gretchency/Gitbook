# Graph 整合

**Palindrome Partitioning**

https://leetcode.com/problems/palindrome-partitioning/
* 对于长度为 n 的字符串，共有 n-1 个隔板可用，每个隔板位置可以选择放或者不放，总共2^(n-1)种可能
* O(2^(n-1)*n)

**Clone Graph**

https://leetcode.com/problems/clone-graph/
* Queue + HashMap

[**Word Ladder**](https://gretchency.gitbooks.io/leetcode/content/wordladder.html)
* BFS 用set去重
* 需要根据size分层，因为每一层都是相同的length
* getNextWords用a-z 26个字母遍历，时间复杂度O(26Ln)


### 拓扑排序


Topological Sorting [link](https://gretchency.gitbooks.io/leetcode/content/topological_sorting.html)
* 判断有无环的话就是最后结果的length是否小于nodes的个数

[Alien Dictionary](https://gretchency.gitbooks.io/leetcode/content/alien_dictionary.html)
* 同一个单词中的字母先后顺序没有任何意义；
* 相邻单词之间，按照 Lexicographical order 排列的意义是，双方字符串中第一个不 match 的字符代表这一条 directed edge，即字符的先后顺序；
* 如果发现字典 Graph 中有环，返回空字符串；
* 加入新入度的时候，记得查重，同一条edge不要重复加入度







### **基础DFS:**




### 树的DFS：

[Path Sum II](https://gretchency.gitbooks.io/leetcode/content/path_sum_ii_shu_de_dfs.html)
* 一定要在符合条件加入结果集后remove一下回溯
* DFS左右子树后再remove一下


**Combination Sum I II III**

两种方法跳过重复数字
* for loop一开始： 
 
 ```if(i > pos && nums[i] == nums[i - 1]) continue;```
 不能i > 0, i == pos时，i处所代表的变量即为某一层遍历中得「第一个元素」，那如果前面的已经用过的元素和i相等，就要跳过
* remove 后：
```while(i < nums.length() - 1 && nums[i] == nums[i + 1]) i++;```
提前预判 避免重复


### 中级DFS



**Generate Parentheses** [leet](https://leetcode.com/problems/generate-parentheses/)

两种情况
* 左括号还没用完
* 左括号比右括号用掉的多 left < right

**Letter Combinations of a Phone Number** [leet](https://leetcode.com/problems/letter-combinations-of-a-phone-number/) [link](https://gretchency.gitbooks.io/leetcode/content/letter_combinations_of_a_phone_number.html)
* index是数字 String[]存字母
* tmp直接添加字符传入递归参数，这样返回后不用截取tmp，就不用remove,自动回溯

***Restore IP Addresses*** [leet](https://leetcode.com/problems/restore-ip-addresses/) [link](https://gretchency.gitbooks.io/leetcode/content/restore_ip_addresses.html)
* 一个字符串，在dfs时候可以减少当前字符串，增加prefix字符串

```dfs(s.substring(i), res, prefix + sub + ".", count + 1);```
* return条件： count == 3 && isValid(s)

***Palindrome Partitioning I*** [link](https://gretchency.gitbooks.io/leetcode/content/palindrome_partitioning_i.html)
* 类比Restore IP Address,我们可以选1个字母，2个字母，直到字符串长度的字母
* 一个字符串，可以本身substring来缩短s长度，s为0时候就return
* substring(beginindex)里beiginindex可以为自身长度，此时返回""



#二维DFS

### [走迷宫问题](https://gretchency.gitbooks.io/leetcode/content/zou_mi_gong_wen_ti_dfs_&_bfs.html)
关于打印路径
* DFS打印路径简单 只要不断记录加入的值，最后reverse一下就行了（reverse是因为深度优先找到结果值才会逐层返回）

* BFS 打印路径就烦一点，要有个map key存符合的点，value存他是从哪个点来的，根据map打印出来 在reverse一下
  * 注意map打包x,y做key的时候要用List<Integer>, array不能作为map的key


**[Surrounded Regions DFS&BFS](https://gretchency.gitbooks.io/leetcode/content/surrounded_regions_dfs&bfs.html)** 
* 类比[Number of Islands](https://leetcode.com/problems/number-of-islands/): 遍历矩阵找1，找到1后count++；dfs周围所有1，标记为2；接着找1
* 发现四条边的O都不能翻牌，就找到这些O并对每个O DFS 找到所有领接的O,把这些O标记成Y
* 遍历矩阵 Y的变回O,还是O的就可以翻牌。

**Word Search**
* 先找到满足第一个字母的点，然后从这个点上下左右DFS
* 注意要记录访问过的点，return时候再变回来

**N-Queen**
* 大体思想就是在每一行放一粒棋子，然后dfs验证可行性
* 分为dfs,验证可行，画棋盘 三个主要函数
* 只需要一个int array存放col位置，其index就是row位置
* 对角线用```Math.abs```
* N-Queen||不能直接把local variable sum放Dfs里面，值会不变。