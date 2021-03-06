# Ugly Number

```
Ugly number is a number that only have factors 2, 3 and 5.

Design an algorithm to find the nth ugly number. 
The first 10 ugly numbers are 1, 2, 3, 4, 5, 6, 8, 9, 10, 12...
```

PQ来poll最小值， hashset来避免重复增加

[http://www.lintcode.com/en/problem/ugly-number-ii/](http://www.lintcode.com/en/problem/ugly-number-ii/)

nlog\(n\)的时间复杂度

```java
public int nthUglyNumber(int n) {
        // write your code here
        if (n <= 0) return -1;
        if (n == 1) return 1;

        Set<Long> set = new HashSet<>();
        PriorityQueue<Long> pq = new PriorityQueue<>();

        set.add((long)1);
        pq.offer((long)1);
        long num = 0;

        long[] primes = new long[3];
        primes[0] = (long)2;
        primes[1] = (long)3;
        primes[2] = (long)5;

        for (int i = 1; i <= n; i++) {
            num = pq.poll();

            for (int j = 0; j < 3; j++) {
                if (!set.contains(primes[j] * num)) {
                    set.add(primes[j] * num);
                    pq.offer(primes[j] * num);
                }
            }
        }

        return (int)num;
    }
```

DP:

[http://wdxtub.com/interview/14520604920730.html](http://wdxtub.com/interview/14520604920730.html)

```java
    public int nthUglyNumber(int n) {
        if (n < 1) return -1;

        int[] dp = new int[n + 1];

        dp[1] = 1;
        int p2 = 1, p3 = 1, p5 = 1;

        for(int i = 2; i <= n; i++) {
            dp[i] = Math.min(dp[p2] * 2, Math.min(dp[p3] * 3, dp[p5] * 5));
            //不能if else,每个都要判断
            if (dp[i] == dp[p2] * 2) p2++;
            if (dp[i] == dp[p3] * 3) p3++;
            if (dp[i] == dp[p5] * 5) p5++;
        }

        return dp[n];
    }
```

## [Super Ugly Number](/Super Ugly Number )

## 注意单独起一个循环判断是否增加index,因为有可能多于一个乘积是相等的

```java
public int nthSuperUglyNumber(int n, int[] primes) {
        // write your code here

        if (n == 0) return -1;

        int[] pIndex = new int[primes.length];
        for (int i = 0; i < primes.length; i++) {
            pIndex[i] = 1;
        }

        int[] res = new int[n + 1];
        res[1] = 1;
        for (int i = 2; i <= n; i++) {
            res[i] = Integer.MAX_VALUE;
            for (int j = 0; j < primes.length; j++) {
                res[i] = Math.min(res[i], res[pIndex[j]] * primes[j]);
            }
            for (int j = 0; j < primes.length; j++) {
                if (res[pIndex[j]] * primes[j] == res[i]) pIndex[j]++;
            }
        }

        return res[n];
    }
```



