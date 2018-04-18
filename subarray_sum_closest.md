# SubArray Sum Closest

## easy:

#### [Subarray Sum](http://www.lintcode.com/en/problem/subarray-sum/#)

sum\[i - j\] = 0  
sum\[j\] - sum\[i - 1\] = 0  
sum\[j\] = sum\[i - 1\]

用HashMap记录当前sum和index, 注意corner case: 先存入\(0, -1\) 解决第一个数为0等情况

## 分析

1. 遍历一遍数组求得子串和
2. 对子串和有小到大排序
3. 相邻两个子串和相减，找到差值的绝对值最小的两个子串和
4. 然后取得subarray的index

注意这里要用Pair class来保存下sum和index，这样最后才能根据sum来获取index

获取index注意

**sum\[i~j\] = sum\[j\] - sum\[i - 1\],所以小的index要加一存入res**

```java
    class Pair {
        int sum;
        int index;
        public Pair(int sum, int index) {
            this.sum = sum;
            this.index = index;
        }
    }

    public int[] subarraySumClosest(int[] nums) {
        //跟subarray sum类似，用一个array存从0到i的sum,然后sort一下，相邻两个找最小的差值
        int[] res = new int[2];
        if (nums == null || nums.length == 0) return res;


        Pair[] sums = new Pair[nums.length];
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            sums[i] = new Pair(sum, i);
        }

        Arrays.sort(sums, new Comparator<Pair>() {
            public int compare(Pair a, Pair b) {
                return a.sum - b.sum;
            }
        });

        int minValue = Integer.MAX_VALUE;

        for (int i = 1; i < sums.length; i++) {
            int currValue = sums[i].sum - sums[i - 1].sum;
            if (minValue > currValue) {
                minValue = currValue;
                //这里用tmp先比较下哪个index小 然后再用res存，因为res里小的数要在前面
                int[] tmp = new int[2];
                tmp[0] = sums[i].index;
                tmp[1] = sums[i - 1].index;
                Arrays.sort(tmp);
                //**小的加一存入res
                res[0] = tmp[0] + 1;
                res[1] = tmp[1];
            }
        }

        return res;
    }
```

### 时间复杂度： O\(nlog\(n\)\)

* 遍历原数组O\(n\)
* sort O\(nlog\(n\)\)
* 遍历pair数组来取得最小差值O\(n\)

总的来说O\(nlog\(n\)\)

### 空间：O\(n\)

* 空间上维护了一个pair数组 O\(n\)



