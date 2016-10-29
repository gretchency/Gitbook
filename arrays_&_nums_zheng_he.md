# Arrays & Nums 整合

Subarray Sum [leet](http://www.lintcode.com/en/problem/subarray-sum/#)
* sum[i ~ j] = sum[j] - sum[i - 1] = 0
* sum[j] = sum[i - 1]
* sumArray Sum k的话 sum[j] - sum[i - 1] = k

Merge Sorted Array [leet](https://leetcode.com/problems/merge-sorted-array/)
* 从后往前比 大的放最后 最后挪B数组剩余的

Maximum Subarray [leet](https://leetcode.com/problems/maximum-subarray/)
* 先区域后全局

Maximum SubarrayII & Best time to buy Stock III
* 中间切一刀 算左右最大

***Sort Colors*** [link](https://gretchency.gitbooks.io/leetcode/content/sort_colors.html)
* 要求排序成red green blue  用三个指针 一个指针记录first not red, 一个用来走，一个记录first not blue,直到走到first not blue为止。

**Subarray Sum Closest** [leet](http://www.lintcode.com/en/problem/subarray-sum-closest/) [link](https://gretchency.gitbooks.io/leetcode/content/subarray_sum_closest.html)
1. 首先遍历一次数组求得子串和。
2. 对子串和排序。
3. 逐个比较相邻两项差值的绝对值，返回差值绝对值最小的两项。

**Longest Consecutive Sequence** [link](https://gretchency.gitbooks.io/leetcode/content/longest_consecutive_sequence.html)
* Hashset 左右找最大可能

[Three Sums Cloest](https://gretchency.gitbooks.io/leetcode/content/three_sum.html)
* 注意比的是3sum和target绝对值之差最小，但返回要返回sum
* 维护与target差值最小的sum，每次比一下差多少，比原sum小就更新
```java
if (Math.abs(sum - target) < Math.abs(min - target)) {
                    min = sum;
         }
```

Partition Array & Sort letters by Case
* Quick Sort思想,返回left

***Median of Two Sorted Array*** [link](https://gretchency.gitbooks.io/leetcode/content/median_of_two_sorted_arrays.html)
* 转换为找第k大个数，再转换为切割掉k/2个数，找k-k/2个数，找到找第一个数
* 切割靠比较A,B数字各自第k/2个数，哪个小就把哪个的左半边割掉，因为这半边肯定没有第k个数
* 如果不够k/2个数，肯定割另一块数组的前k/2个数
* base case是k只剩1，比较第一个点就行

---


Set Matrix Zeroes [link](https://gretchency.gitbooks.io/leetcode/content/wei_ruan.html)
* O(m*n) 建立克隆矩阵 放0
* O(m+n) 对行和列建立两个boolean数组，一旦扫到0就标记该行列boolean为
* O(1) 用第0行第0列记录每行每列要不要放0，然后从(1, 1)开始遍历。同时两个boolean变量记录第0行第0列是否要变0。

[Majority Elements](https://gretchency.gitbooks.io/leetcode/content/majority_number.html)
* 搞一个计数器，让每一个数和其他数pk，还是他就计数器++,不是他就计数器--,最后看还存活下来的数是谁

Plus One
* 维护Carry从后往前走， 如果到最后一位还有carry,直接new一个len+1的数组，第一位是carry,然后return

[Container With Most Water](https://gretchency.gitbooks.io/leetcode/content/container_with_most_water.html)
典型双指针问题

* 注意短板理论: 
  * ```height[left] < height[right] left++``` 因为移动left可能变大，而移动right只会变小，因为left是短板，高固定死了,没法补救。反之亦然。


[Happy Number](https://gretchency.gitbooks.io/leetcode/content/happy_number.html)
* 用HashSet检查重复，如果有重复数字就会陷入死循环，这就不是Happy Number，直到算出和为1

Palindrome Number
* 回文数翻转后和原来的数一样
```java
int rev = 0;
while (x != 0) {
    rev = rev * 10 + x % 10;
    x /= 10;
}
```

Rotate Array
* 注意k可能超出array的length，要先%一下
* 先全局reverse,再分两个局部reverse






