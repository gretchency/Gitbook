# Data Structure整合
***LRU CACHE*** [LINK](https://gretchency.gitbooks.io/leetcode/content/lru_cache.html)
* 根据题意要存放node,每个node都有key, val，所以根据此建立node class
* 由于node删除操作要知道前后的点，所以用doubly linked list
* 注意capacity满了以后 不仅要删除第一个node 还要删除map的对应node!
* set时候如果Cache里已经有key，要更新value!

---

### Priority Queue:
Ugly Number ||
* PQ + HashSet 注意要用Long防止溢出！
* pq用来排序,set用来判断是否重复

**Merge k Sorted Lists & Merge k sorted array** [leet](https://leetcode.com/problems/merge-k-sorted-lists/) [link](https://gretchency.gitbooks.io/leetcode/content/merge_k_sorted_linkedlist.html)
* 注意List里面可能有null节点，此时要跳过

**Top K Frequent Elements** [leet](https://leetcode.com/problems/top-k-frequent-elements/)
* 取pq的最小值和新的比较
* HashMap + Min_Heap 注意Map的遍历写法 O(nlog(k))


Meeting Room II
* 给一堆时间 求最少需要几个meeting room
* 利用最小堆将能合并的开会时间合并到一个屋子，计算需要几个屋子


---
### Hashing


Rehashing [leet](http://www.lintcode.com/en/problem/rehashing/)
* 注意在rehashing时候要考虑新table是否已经有数，已经有数的情况下用dummy node遍历到末尾再接上。


---



### Queue & Stack



Implement Queue By two stacks
* 一个用来push 一个用来pop peek, 
* LILO + LILO = FIFO 把s1的所有元素加入s2，s2的顺序就是FIFO的


**Largest Rectangle in Histogram	**
* 遍历全部高度， 找每个数左右第一个比他小的数在哪
* 维护一个**递增栈**，发现比栈顶小的时候就计算面积
* stack存index,如果stack直接存高度会丢失index信息