# 刷题日志


## Sep.24


今天刷了四道dfs 

Friends Dictionary Permutation相关

实在太菜 读小土刀的刷题总结





## Ladder


### Pre

**Implement strStr()** [leet](https://leetcode.com/problems/implement-strstr/)




### Binary Search

**Search Insert Position** [leet](https://leetcode.com/problems/search-insert-position/)
* find first position that value is >= target

**Search a 2D Matrix** [leet](https://leetcode.com/problems/search-a-2d-matrix/)
* matrix[mid / col][mid % col] == target
* Search a 2D Matrix II: left bottom to top right

**First Position of Target**
```java
if (nums[mid] == target)
                //cannot return, cuz it may not be the first position
                end = mid;
```

**Search in a big Sorted Array** [leet](https://adambillylee.gitbooks.io/lintcode/content/chapter2.3.html)

```java
// find an end to start with
    while(reader.get(end) != -1 && reader.get(end)<target) {
        end = end * 2 + 1;
    }
```

Find Minimum in Rotated Sorted Array
* find first position <= the last number

**Search in Rotated Sorted Array**
* 注意截取的时候 ```target >= nums[start] && target <= nums[mid]``` 才能保证在那一小段里

**Find Peak Element**
* 砍掉一半的方法
* 根据题意，该数组必定至少存在一个peak,由此可知若A[mid - 1] > A[mid],peak在mid左半边，A[mid] < A[mid + 1],peak在右半边，由此可求得Peak.

**Search for a Range**
* 两次二分，找first position和last postion










### Binary Tree
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

















### DP I

Unique Paths I

Unique Paths II
* 判断如果 ==1 路径数为0

Climbing Stairs

Minimum Path Sum

Triangle
* 三角形两边初始化，top-down，比较最后一行

Jump Game I
* 注意循环里一旦为True就break

Jump Game II
* dp[i] = Min(dp[j] + 1) && j + nums[j] >= i:循环j比较当前i的最小值
* 或者从头开始走j走到第一个满足的就是最小值 break;

***Longest Increasing Subsequence***
* dp[i]代表前i个数字中以第i个数结尾的lis
* 然后逐个比较dp[i]
* 有的时候dp问题的解决需要找到问题的根源，而不是一味的简单求解



### DP II
**Edit Distance** [leet](https://leetcode.com/problems/edit-distance/)
* dp[i][j] 分为最后一位相等或不等两种情况

***Distinct Subsequences*** [leet](https://leetcode.com/problems/distinct-subsequences/)
* dp[i][j] 分为最后一位相等或不等两种情况
* 最后一位不等靠前面dp[i - 1][j]
* 最后一位相等：dp[i - 1][j - 1] + dp[i - 1][j]

**Longest Common Subsequences** [link](https://gretchency.gitbooks.io/leetcode/content/longest_common_subsequence.html)
* dp[i][j] 分为最后一位相等或不等两种情况
* 如果最后一位俩字符不相等，那么他俩就不可能同时出现在subsequence当中，根据这一特性缩小范围。

Longest Common Substring
* substring必须要相连，所以普通状态转移不行
* dp[i][j]表示A的前i个字符和B的前j个字符的LCS且**A[i - 1] == B[j - 1]**,否则清0重新算
* 最后双重循环找到最大的

***Interleaving String*** [link](https://gretchency.gitbooks.io/leetcode/content/interleaving_string.html)

S1 S2 能否凑成 S3
状态：s1的前i个字符和s2的前j个字符能否凑成s3的前i+j个字符

* 状态方程dp[i][j]满足两种条件：
* 由于S3的每一位都由s1或s2中相应位置字符构成

1. dp[i - 1][j] 然后s1和s3相应位置最后一位相等
2. dp[i][j - 1] 然后s2和s3相应位置最后一位相等


Word Break
* i - j <= MaxLen 来节省时间

***Palindrome Partitioning II***
* 区间动归来省时间 O(n^2)
* 序列动归：ispal(s(j~i-1)) dp[i] = min(dp[i], dp[j] + 1)
* 区间动归的for loop很有特色 第一层**for len**, 第二层for start，这杨才能保证start不越界并且慢慢增加区间长度


### LinkedList

Remove Nth Node From End of List
* 在删除节点的前一个节点停住 while (fast.next != null)

Partition List [leet](https://leetcode.com/problems/partition-list/)
* two dummy node & 注意这里原链表可能big后面还有点 要把他指向空

Remove Duplicates from Sorted List II
* 如果相等存一个value 和head.next比较

Convert Sorted Array to Binary Search Tree

***Convert Sorted List to Binary Search Tree***
[leet](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/) [link](https://gretchency.gitbooks.io/leetcode/content/convert_sorted_list_to_balanced_bst.html)
* 每个链表节点被访问一次，故时间复杂度为 O(n)
* 分治法 利用len求得链表的中点 注意右边的Len = len - len/2 - 1 分别减去左子树长度和根节点

**Copy list with Random Pointer**
* HashMap记录深拷贝映射关系
* 运用dummy和curr node往下copy
* Map处理映射关系，先copy链表元素再copy Random指针指向元素，每次copy前在map里判断是否已经生成，避免出现重复节点

Sort List
* MergeSort
* 注意先判断head是否只有一个节点
* merge里面判断lList或者rList是否没走完完用if， while会死循环！

***Reorder List*** [leet](https://leetcode.com/problems/reorder-list/)
* 快慢指针找中点，分成左右两半
* 把右半边reverse
* 左右一一Merge,注意merge的时候，小心处理链表节点的断开及链接！next value要处理前先存成tmp.

Reverse Linked List II
* 注意最后首尾相连
* 遍历过程中要存放preM和mNode
* preM和prev连首部，mNode和curr连尾部





### Arrays & Numbers

Subarray Sum [leet](http://www.lintcode.com/en/problem/subarray-sum/#)
* sum[i ~ j] = sum[j] - sum[i - 1] = 0
* sum[j] = sum[i - 1]
* sumArray Sum k的话 sum[j] - sum[i - 1] = k

Merge Sorted Array [leet](https://leetcode.com/problems/merge-sorted-array/)
* 从后往前比 大的放最后 最后挪B数组剩余的

Maximum Subarray [leet](https://leetcode.com/problems/maximum-subarray/)
* 先区域后全局

Maximum SubarrayII & Best time to buy Stock III

***Sort Colors*** [link](https://gretchency.gitbooks.io/leetcode/content/sort_colors.html)
* 要求排序成red green blue  用三个指针 一个指针记录first not red, 一个用来走，一个记录first not blue,直到走到first not blue为止。

**Subarray Sum Closest** [leet](http://www.lintcode.com/en/problem/subarray-sum-closest/) [link](https://gretchency.gitbooks.io/leetcode/content/subarray_sum_closest.html)
1. 首先遍历一次数组求得子串和。
2. 对子串和排序。
3. 逐个比较相邻两项差值的绝对值，返回差值绝对值最小的两项。

**Longest Consecutive Sequence** [link](https://gretchency.gitbooks.io/leetcode/content/longest_consecutive_sequence.html)
* Hashset 左右找最大可能

Three Sums Cloest
* 注意比的是3sum和target绝对值之差最小，但返回要返回sum
```java
if (Math.abs(sum - target) < Math.abs(min - target)) {
                    min = sum;
         }
```

Set Matrix Zeroes [link](https://gretchency.gitbooks.io/leetcode/content/wei_ruan.html)
* O(m*n) 建立克隆矩阵 放0
* O(m+n) 对行和列建立两个boolean数组，一旦扫到0就标记该行列boolean为
* O(1) 用第0行第0列记录每行每列要不要放0，然后从(1, 1)开始遍历。同时两个boolean变量记录第0行第0列是否要变0。


 
 







### Data Structure

**Merge k Sorted Lists & Merge k sorted array** [leet](https://leetcode.com/problems/merge-k-sorted-lists/) [link](https://gretchency.gitbooks.io/leetcode/content/merge_k_sorted_linkedlist.html)
* 注意List里面可能有null节点，此时要跳过



**Top K Frequent Elements** [leet](https://leetcode.com/problems/top-k-frequent-elements/)
* 取pq的最小值和新的比较
* HashMap + Min_Heap 注意Map的遍历写法 O(nlog(k))

Rehashing [leet](http://www.lintcode.com/en/problem/rehashing/)
* 注意在rehashing时候要考虑新table是否已经有数，已经有数的情况下用dummy node遍历到末尾再接上。


### Graph & Search
**Palindrome Partitioning**

https://leetcode.com/problems/palindrome-partitioning/
* 对于长度为 n 的字符串，共有 n-1 个隔板可用，每个隔板位置可以选择放或者不放，总共2^(n-1)种可能
* O(2^(n-1)*n)

**Clone Graph**

https://leetcode.com/problems/clone-graph/
* Queue + HashMap

Topological Sorting [link](https://gretchency.gitbooks.io/leetcode/content/topological_sorting.html)
* 判断有无环的话就是最后结果的length是否小于nodes的个数

**基础DFS:**

Combination Sum I II III
两种方法跳过重复数字
* for loop一开始： 
 
 ```if(i > pos && nums[i] == nums[i - 1]) continue;```
 不能i > 0, i == pos时，i处所代表的变量即为某一层遍历中得「第一个元素」，那如果前面的已经用过的元素和i相等，就要跳过
* remove 后：
```while(i < nums.length() - 1 && nums[i] == nums[i + 1]) i++;```
提前预判 避免重复

中级DFS

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

二维DFS

**Surrounded Regions DFS&BFS** [link](https://gretchency.gitbooks.io/leetcode/content/surrounded_regions_dfs&bfs.html)
* 类比[Number of Islands](https://leetcode.com/problems/number-of-islands/): 遍历矩阵找1，找到1后count++；dfs周围所有1，标记为2；接着找1
* 发现四条边的O都不能翻牌，就找到这些O并对每个O DFS 找到所有领接的O,把这些O标记成Y
* 遍历矩阵 Y的变回O,还是O的就可以翻牌。












































































