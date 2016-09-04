# Median of Two Sorted Arrays

http://www.lintcode.com/en/problem/median-of-two-sorted-arrays/

![](Screen Shot 2016-09-04 at 7.28.37 PM.png)

时间复杂度：
log(m + n / 2) log(k)

```
    //log(m + n / 2)
    //换成找到第k个点思考
    public double findMedianSortedArrays(int[] A, int[] B) {
        int length = A.length + B.length;
        if (length % 2 == 1) {
            return findKth(A, 0, B, 0, length / 2 + 1);
        } else {
            return (findKth(A, 0, B, 0, length / 2) + findKth (A, 0, B, 0, length / 2 + 1)) / 2.0;
        }
        

    }
    
    private int findKth(int[] A, int A_start, int[] B, int B_start, int k) {
        //A全舍弃了
        if (A_start >= A.length) {
            return B[B_start + k - 1];
        }
        
        
        //B全舍弃了
        if (B_start >= B.length) {
            return A[A_start + k - 1];
        }
        
        //找第一个点
        if (k == 1) {
            return Math.min(A[A_start], B[B_start]);
        }
        
        int A_key;
        int B_key;
        
        //找到A的k / 2点
        if ((A_start + k / 2 - 1) < A.length) {
            A_key = A[A_start + k / 2 - 1];
        } else {
            A_key = Integer.MAX_VALUE;
        }
        
        //找到B的k / 2点
        if ((B_start + k / 2 - 1) < B.length) {
            B_key = B[B_start + k / 2 - 1];
        } else {
            B_key = Integer.MAX_VALUE;
        }
        

        如果A小于B，舍弃A的前半断,k缩短为k - k / 2
        if (A_key < B_key) {
            return findKth(A, A_start + k / 2, B, B_start, k - k / 2);
        } else {
            return findKth(A, A_start, B, B_start + k / 2, k - k / 2);
        }
    }
```