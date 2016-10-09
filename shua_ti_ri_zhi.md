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





### Binary Tree
Maximum depth of a Binary Tree

Binary Tree Preorder Travesal

***Binary Tree Maximum Path Sum*** [leet](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

* 全局变量的使用

inorder successor in binary search tree
* inorder travesal 在traversal的过程中有一个Boolean 一开始false 后面相等时变true,下一个节点就是successor







### DP I

Unique Paths I

Unique Paths II
* 判断如果 ==1 路径数为0

Climbing Stairs

Minimum Path Sum


### DP II
**Edit Distance** [leet](https://leetcode.com/problems/edit-distance/)
* dp[i][j] 分为最后一位相等或不等两种情况

**Distinct Subsequences** [leet](https://leetcode.com/problems/distinct-subsequences/)
* dp[i][j] 分为最后一位相等或不等两种情况

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




### Arrays & Numbers

Subarray Sum [leet](http://www.lintcode.com/en/problem/subarray-sum/#)
* sum[i ~ j] = sum[j] - sum[i - 1] = 0
* sum[j] = sum[i - 1]
* sumArray Sum k的话 sum[j] - sum[i - 1] = k

Merge Sorted Array [leet](https://leetcode.com/problems/merge-sorted-array/)
* 从后往前比 大的放最后 最后挪B数组剩余的

Maximum Subarray [leet](https://leetcode.com/problems/maximum-subarray/)

***Sort Colors*** [link](https://gretchency.gitbooks.io/leetcode/content/sort_colors.html)
* 要求排序成red green blue  用三个指针 一个指针记录first not red, 一个用来走，一个记录first not blue,直到走到first not blue为止。

**Subarray Sum Closest** [leet](http://www.lintcode.com/en/problem/subarray-sum-closest/) [link](https://gretchency.gitbooks.io/leetcode/content/subarray_sum_closest.html)
1. 首先遍历一次数组求得子串和。
2. 对子串和排序。
3. 逐个比较相邻两项差值的绝对值，返回差值绝对值最小的两项。

**Longest Consecutive Sequence** [link](https://gretchency.gitbooks.io/leetcode/content/longest_consecutive_sequence.html)
* Hashset 左右找最大可能



 
 







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










































































