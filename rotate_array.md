# Rotate Array

```
Rotate an array of n elements to the right by k steps.
For example, with n = 7 and k = 3, 
the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].

Note: Try to come up as many solutions as you can, 
there are at least 3 different ways to solve this problem.
```

* 注意k可能超出array的length，要先%一下
* 先全局reverse,再分两个局部reverse

```java
public class Solution {
    public void rotate(int[] nums, int k) {
        if (nums == null || nums.length < 2) return;
        
        k = k % nums.length;
        
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
        
    }
    
    private void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int tmp = nums[start];
            nums[start] = nums[end];
            nums[end] = tmp;
            start++;
            end--;
        }
    }
}
```


Solution 2:

将被覆盖的部分存到临时数组
