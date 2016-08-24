# Climbing Stairs

http://www.lintcode.com/en/problem/climbing-stairs/#


You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

题目问的是到达顶端的方法数，我们采用序列类问题的通用分析方法，可以得到如下四要素：

State: f[i] 爬到第i级的方法数

Function: f[i]=f[i-1]+f[i-2]

Initialization: f[0]=1,f[1]=1

Answer: f[n]

尤其注意状态转移方程的写法，f[i]只可能由两个中间状态转化而来，一个是f[i-1]，由f[i-1]到f[i]其方法总数并未增加；另一个是f[i-2]，由f [i-2]到f[i]隔了两个台阶，因此有1+1和2两个方法，因此容易写成 f[i]=f[i-1]+f[i-2]+1，但仔细分析后能发现，由f[i-2]到f[ i]的中间状态f[i-1]已经被利用过一次，故f[i]=f[i-1]+f[i-2]

```java
public int climbStairs(int n) {

        
        if (n <= 1) {
            return 1;
        }
        
        //State: f[i] 爬到第i级的方法数
        
        //注意初始化n+1!
        int[] mem = new int[n + 1];
        
        //Initialization: f[0]=1,f[1]=1
        mem[0] = 1;
        mem[1] = 1;
        
        //Function: f[i]=f[i-1]+f[i-2]
        for(int i = 2; i <= n; i++){
            mem[i] = mem[i-1] + mem[i-2];
         }
         
        //Answer: f[n]
        return mem[n];
    }
```