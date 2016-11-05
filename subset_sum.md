# Subset Sum

Given a set of non-negative integers, and a value sum, determine if there is a subset of the given set with sum equal to given sum.

```
Examples: set[] = {3, 34, 4, 12, 5, 2}, sum = 9
Output:  True  //There is a subset (4, 5) with sum 9.
```

Naive Recurrsive Way
```java
 static boolean isSubsetSumRecurrsive(int[] set, int sum) {
        if (set == null || set.length == 0) return false;
        
        int n = set.length;
        
        
        return helper(set, n, sum);
    }
    
    static boolean helper(int[] set, int n, int sum) {
        if (sum == 0) return true;
        if (n == 0) return false;
        
        //如果最后一位比sum大， ignore it
        if (set[n - 1] > sum) return helper(set, n - 1, sum);
        
        //ignore last element or substrat the last element 
        return helper(set, n - 1 , sum) || helper(set, n - 1, sum - set[n - 1]);
    }
```