# data stream median (2 PQ)

http://www.lintcode.com/en/problem/data-stream-median/

用两个堆, max heap 和 min heap. 维持两个堆的大小相等(max堆可以比min堆多一个).  则max堆的顶即为median值. 


```java
public class Solution {
    /**
     * @param nums: A list of integers.
     * @return: the median of numbers
     */
     
    private PriorityQueue<Integer> maxQ, minQ;
    
    public int[] medianII(int[] nums) {        
        Comparator<Integer> comp = new Comparator<Integer>() {
            
            @Override
            public int compare(Integer n1, Integer n2) {
                return n2 - n1;
            }
        };
        
        int len = nums.length;
        
        maxQ = new PriorityQueue<Integer>(len, comp);
        minQ = new PriorityQueue<Integer>(len);
        
        int[] ans = new int[len];
        
        ans[0] = nums[0];
        maxQ.offer(ans[0]);
        
        for (int i = 1; i < len; i++) {
            addNumber(nums[i]);
            ans[i] = getMid();
        }
        
        return ans;
    }
    
    private void addNumber(int num){
        int x = maxQ.peek();
        if (num <= x) {
            maxQ.offer(num);
        } else {
            minQ.offer(num);
        }
        //用两个堆, max heap 和 min heap. 维持两个堆的大小相等(max堆可以比min堆多一个).  则max堆的顶即为median值. 
        if (maxQ.size() - minQ.size() > 1) {
            minQ.offer(maxQ.poll());
        } else if (maxQ.size() < minQ.size()) {
            maxQ.offer(minQ.poll());
        }
        
    }
    
    private int getMid() {
        return maxQ.peek();
    }
}
```

巧妙解法

max queue is always larger or equal to min queue


```java
    public void addNum(int num) {
        max.offer(num);
        min.offer(max.poll());
        if (max.size() < min.size()){
            max.offer(min.poll());
        }
    }
```