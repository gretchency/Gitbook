# Kth Largest Element

1. Quick Sort: O\(nlog\(n\)\), O\(1\)
2. Min Heap: O\(nlog\(k\)\), O\(k\)
3. Quick Select: O\(n\), O\(1\)    \(worst: O\(n^2\), O\(1\)

Quick Select:

* 找第k大，用倒序，找第k-1个数
* Quick Sort相同思路，只是每次选择一半，如果`k <= 右指针j`，说明k在左边的一半（left, j），如果`k >=左指针i`， 说明k在右边一半\(i,right\), 若都不是，说明k就在pivot位置
* [Why O\(n\)](https://stackoverflow.com/questions/8783408/why-is-the-runtime-of-the-selection-algorithm-on?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)?
  * n + n/2+n/4+...+1\(log\(n\) times\) = 2n

```java
public class Solution {
    public int findKthLargest(int[] nums, int k) {
        return quickSelect(nums, k - 1, 0, nums.length - 1);
    }

    private int quickSelect(int[] nums, int k, int left, int right) {
        if (left >= right) return nums[k];

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
        //此时k就是已经排好序的pivot
        return pivot;
    }

    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```

Related:

## [Median](http://www.lintcode.com/en/problem/median/)

找中间大的数

```java
public int median(int[] nums) {
        // write your code here
        if (nums == null || nums.length == 0) return -1;

        if (nums.length % 2 == 1) {
            return findKthNum(nums, 0, nums.length - 1, nums.length / 2);
        } else {
            return findKthNum(nums, 0, nums.length - 1, nums.length / 2 - 1);
        }
    }

    private int findKthNum(int[] nums, int start, int end, int k) {
        if (start == end) return nums[k];

        int i = start;
        int j = end;
        int pivot = nums[start + (end - start) / 2];
        while (i <= j) {
            while (i <= j && nums[i] < pivot) {
                i++;
            }

            while (i <= j && nums[j] > pivot) {
                j--;
            }

            if (i <= j) {
                swap(nums, i, j);
                i++;
                j--;
            }
        }

        if (k <= j) return findKthNum(nums, start, j, k);
        if (k >= i) return findKthNum(nums, i, end, k);
        return pivot;
    }

    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
```



