# DP 整合


### LADDER

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

---

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

---