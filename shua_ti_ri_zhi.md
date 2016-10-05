# 刷题日志


## Sep.24


今天刷了四道dfs 

Friends Dictionary Permutation相关

实在太菜 读小土刀的刷题总结





## Ladder


### Pre

**Implement strStr()**

https://leetcode.com/problems/implement-strstr/


### Binary Search

**Search Insert Position**

https://leetcode.com/problems/search-insert-position/
* find first position that value is >= target

**Search a 2D Matrix**

https://leetcode.com/problems/search-a-2d-matrix/
* matrix[mid / col][mid % col] == target
* Search a 2D Matrix II: left bottom to top right




### Binary Tree
Maximum depth of a Binary Tree

Binary Tree Preorder Traveral


### DP I

Unique Paths I

Unique Paths II
* 判断如果 ==1 路径数为0


### DP II
**Edit Distance**

https://leetcode.com/problems/edit-distance/
* dp[i][j] 分为最后一位相等或不等两种情况

**Distinct Subsequences
**
https://leetcode.com/problems/distinct-subsequences/
* dp[i][j] 分为最后一位相等或不等两种情况


### LinkedList

Remove Nth Node From End of List
* 在删除节点的前一个节点停住 while (fast.next != null)

Partition List

https://leetcode.com/problems/partition-list/

* two dummy node & 注意这里原链表可能big后面还有点 要把他指向空


### Arrays & Numbers

Subarray Sum

http://www.lintcode.com/en/problem/subarray-sum/#

* sum[i ~ j] = sum[j] - sum[i - 1] = 0
* sum[j] = sum[i - 1]
* sumArray Sum k的话 sum[j] - sum[i - 1] = k












































