# Kth Largest Element

1. Quick Sort: O(nlog(n)), O(1)
2. Min Heap: O(nlog(k)), O(k)
3. Quick Select: O(n), O(1)    (worst: O(n^2), O(1)


Quick Select:

```java
public class Solution {
    public int findKthLargest(int[] nums, int k) {
        return quickSelect(nums, k - 1, 0, nums.length - 1);
    }
    
    private int quickSelect(int[] nums, int k, int left, int right) {
        if (left == right) return nums[k];
        
        int pivot = nums[left + (right - left) / 2];
        int i = left;
        int j = right;
        while (i <= j) {
            while (i <= j && nums[i] > pivot) {
                i++;
            }
            
            while (i <= j && nums[j] < pivot) {
                j--;
            }
            
            if (i <= j) {
                swap(nums, i, j);
                i++;
                j--;
            }
        }
        
        if (k <= j) return quickSelect(nums, k, left, j);
        if (k >= i) return quickSelect(nums, k, i, right);
        //此时k就是pivot位置
        return nums[k];
    }
    
    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```