# DP 整合

### LADDER

### DP （坐标型：小人在跳来跳去/ 矩阵型）

Unique Paths I

Unique Paths II

* 判断如果 ==1 路径数为0

Minimum Path Sum

Triangle

* 三角形两边初始化，top-down，比较最后一行

_**Longest Increasing Subsequence**_

* dp\[i\]代表前i个数字中以第i个数结尾的lis
* 然后逐个比较dp\[i\]
* 有的时候dp问题的解决需要找到问题的根源，而不是一味的简单求解

---

### 单序列DP

Climbing Stairs

Jump Game I

* 注意循环里一旦为True就break

Jump Game II

* dp\[i\] = Min\(dp\[j\] + 1\) && j + nums\[j\] &gt;= i:循环j比较当前i的最小值
* 或者从头开始走j走到第一个满足的就是最小值 break;

Word Break

* i - j &lt;= MaxLen 来节省时间

[_**Palindrome Partitioning II**_](https://gretchency.gitbooks.io/leetcode/content/palindrome_partitioning_ii.html)

* 区间动归来省时间 O\(n^2\)
* 序列动归：ispal\(s\(j~i-1\)\) dp\[i\] = min\(dp\[i\], dp\[j\] + 1\)
* 区间动归的for loop很有特色 第一层**for len**, 第二层for start，这杨才能保证start不越界并且慢慢增加区间长度

[House Robber](https://gretchency.gitbooks.io/leetcode/content/house_robber.html)

* 要么搜刮当前家，放弃前一家，要么搜刮前一家，放弃当前家
  * dp\[i\] = max\(dp\[i - 2\] + num\[i\], dp\[i - 1\]\)
* RobberII成环的情况下，就是用两个dp，比比不要第一家和不要最后一家谁大

[Coin Change](https://gretchency.gitbooks.io/leetcode/content/coin_change.html)

* dp\[i\]表示达到i面额需要的最少硬币数，初始化为无限大
* 要么不用当前硬币，要么用到当前硬币，比较哪个需要的硬币少
* dp\[i\] = min\(dp\[i\], dp\[i - coins\[j\]\] + 1\)

### 双序列DP

**Edit Distance** [leet](https://leetcode.com/problems/edit-distance/)

* dp\[i\]\[j\] 分为最后一位相等或不等两种情况

_**Distinct Subsequences**_ [leet](https://leetcode.com/problems/distinct-subsequences/)

* dp\[i\]\[j\] 分为最后一位相等或不等两种情况
* 最后一位不等靠前面dp\[i - 1\]\[j\]
* 最后一位相等：dp\[i - 1\]\[j - 1\] + dp\[i - 1\]\[j\]

**Longest Common Subsequences** [link](https://gretchency.gitbooks.io/leetcode/content/longest_common_subsequence.html)

* dp\[i\]\[j\] 分为最后一位相等或不等两种情况
* 如果最后一位俩字符不相等，那么他俩就不可能同时出现在subsequence当中，根据这一特性缩小范围。

Longest Common Substring

* substring必须要相连，所以普通状态转移不行
* dp\[i\]\[j\]表示A的前i个字符和B的前j个字符的LCS且**A\[i - 1\] == B\[j - 1\]**,否则不连续不构成substring，清0重新算

* 最后双重循环找到最大的

_**Interleaving String**_ [link](https://gretchency.gitbooks.io/leetcode/content/interleaving_string.html)

S1 S2 能否凑成 S3  
状态：s1的前i个字符和s2的前j个字符能否凑成s3的前i+j个字符

* 状态方程dp\[i\]\[j\]满足两种条件：
* 由于S3的每一位都由s1或s2中相应位置字符构成

* dp\[i - 1\]\[j\] 然后s1和s3相应位置最后一位相等

* dp\[i\]\[j - 1\] 然后s2和s3相应位置最后一位相等

---

[Subset Sum](https://gretchency.gitbooks.io/leetcode/content/subset_sum.html)  
dp\[i\]\[j\]代表sum为i时，是否能从set\[0\]~set\[j-1\]个数中相加得到sum

### DPIII \(区间型\)

### [Coins in a line](https://gretchency.gitbooks.io/leetcode/content/coins_in_a_line.html)

经典区间动归

* dp\[i\]\[j\] 代表从i到j这个区间取到的最大金币
* 初始化：
  * i和j一样时候就取coins\[i\]
  * i和j相邻去max\(coins\[i\], coins\[j\]\)
* 方程：
  * 比较取左取右哪个大，取左的话，再加上等待对手取完多的金币的那一部分，取右同理（因为假设对手很聪明，他肯定会取剩下的里多的金币，那你只能取剩下的那块区间）



