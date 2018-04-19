# SubArray Sum Closest

## easy:

#### [Subarray Sum](http://www.lintcode.com/en/problem/subarray-sum/#)

sum\[i - j\] = 0  
sum\[j\] - sum\[i - 1\] = 0  
sum\[j\] = sum\[i - 1\]

用HashMap记录当前sum和index, 注意corner case: 先存入\(0, -1\) 解决第一个数为0等情况

## SubArray Sum Closest

## 分析

1. 遍历一遍数组求得子串和
2. 要找数组中最接近的两个数，需要排序
3. 对子串和有小到大排序
4. 相邻两个子串和相减，找到差值的绝对值最小的两个子串和
5. 然后取得subarray的index

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

public class Solution {

    /*
     * @param nums: A list of integers
     * @return: A list of integers includes the index of the first number and the index of the last number
     */
    public int[] subarraySumClosest(int[] nums) {
        // write your code here
        int[] res = new int[2];
        if (nums == null || nums.length <= 1) return res;
        
        int sum = 0;
        
        Pair[] sumArray = new Pair[nums.length];
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            Pair pair = new Pair(sum, i);
            sumArray[i] = pair;
        }
        
        Arrays.sort(sumArray, pairComparator);
        
        int minVal = Integer.MAX_VALUE;
        int tmp[] = new int[2];
        for (int i = 1; i < nums.length; i++) {
            int currVal = sumArray[i].sum - sumArray[i - 1].sum;
            if (currVal < minVal) {
                minVal = currVal;
                tmp[0] = sumArray[i].index;
                tmp[1] = sumArray[i - 1].index;
            }
        }
        
        //谁小谁大不一定，要排序
        Arrays.sort(tmp);
        
        //sum[i~j] = sum[j] - sum[i - 1] 所以res的index为sum的index加1
        res[0] = tmp[0] + 1;
        res[1] = tmp[1];
        
        return res;
    }
    
    private Comparator<Pair> pairComparator = new Comparator<Pair>() {
        @Override
        public int compare(Pair p1, Pair p2) {
            return p1.sum - p2.sum;
        }
    }; 
}
```

### 时间复杂度： O\(nlog\(n\)\)

* 遍历原数组O\(n\)
* sort O\(nlog\(n\)\)
* 遍历pair数组来取得最小差值O\(n\)

总的来说O\(nlog\(n\)\)

### 空间：O\(n\)

* 空间上维护了一个pair数组 O\(n\)



