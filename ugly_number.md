# Ugly Number

PQ来poll最小值， hashset来避免重复增加

http://www.lintcode.com/en/problem/ugly-number-ii/

nlog(n)的时间复杂度

```java
class Solution {
    /**
     * @param n an integer
     * @return the nth prime number as description.
     */
    public int nthUglyNumber(int n) {
        // HashSet + PQ
        
        PriorityQueue<Long> pq = new PriorityQueue<Long>();
        HashSet<Long> set = new HashSet<Long>();
        
        Long[] prime = new Long[3];
        prime[0] = Long.valueOf(2);
        prime[1] = Long.valueOf(3);
        prime[2] = Long.valueOf(5);
        
        for (int i = 0; i < 3; i++) {
            pq.offer(prime[i]);
            set.add(prime[i]);
        }
        
        //第一个数是1
        Long number = Long.valueOf(1);
        
        //注意从i = 1开始
        for (int i = 1; i < n; i++) {
            number = pq.poll();
            for (int j = 0; j < 3; j++) {
                if (!set.contains(prime[j] * number)) {
                    pq.offer(prime[j] * number);
                    set.add(prime[j] * number);
                }
            }
        }
        
        return number.intValue();
    }
};
```