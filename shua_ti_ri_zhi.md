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





### Data Structure

**Merge k Sorted Lists & Merge k sorted array**

https://leetcode.com/problems/merge-k-sorted-lists/

**Top K Frequent Elements**

https://leetcode.com/problems/top-k-frequent-elements/
* HashMap + Min_Heap 注意Map的遍历写法 O(nlog(k))


### Graph & Search
**Palindrome Partitioning**

https://leetcode.com/problems/palindrome-partitioning/
* 对于长度为 n 的字符串，共有 n-1 个隔板可用，每个隔板位置可以选择放或者不放，总共有$$2^{n-1}$$种可能
* O($$2^{n-1}$$* n)

**Clone Graph**

https://leetcode.com/problems/clone-graph/
* Queue + HashMap
































































