# Merge Sorted Array

http://www.lintcode.com/en/problem/merge-sorted-array/

从尾部merge O(n)的复杂度

![](Screen Shot 2016-09-04 at 3.31.45 PM.png)


```java
public void mergeSortedArray(int[] A, int m, int[] B, int n) {
        
        int i = m - 1;
        int j = n - 1;
        int index = m + n - 1;
        
        while (i >= 0 && j >= 0) {
            if (A[i] > B[j]) {
                //执行完当前比较后--
                A[index--] = A[i--];
            } else {
                A[index--] = B[j--];
            }
        }
        
        while (i >= 0) {
            A[index--] = A[i--];
        }
        
        while (j >= 0) {
            A[index--] = B[j--];
        }
    }
```