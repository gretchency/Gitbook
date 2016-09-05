# Wood Cut(二分答案）

http://www.lintcode.com/en/problem/wood-cut/

思路：
最大不可能超过L[i]的最大值

然后二分答案， 得到长度大于k就提高答案， 小于k就缩小答案

最后return start 或 end 得到的长度


```java
    //二分答案
    
    public int woodCut(int[] L, int k) {
        int max = 0;
        for (int i = 0; i < L.length; i++) {
            max = Math.max(max, L[i]);
        }
        
        //start从1开始
        int start = 1;
        int end = max;
        
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            
            if (count(L, mid) >= k) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (count(L, end) >= k) {
            return end;
        }
        
        if (count(L, start) >= k) {
            return start;
        } 
        
        return 0;
    }
    
    private int count(int[] L, int length) {
        int sum = 0;
        for (int i = 0; i < L.length; i++) {
            int count = L[i] / length;
            sum += count;
        }
        
        return sum;
    }
```