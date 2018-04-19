# Sort Colors

左右指针记录边界

二刷

* 先把0，2的走完 这样逻辑更清楚

  ```java
  public class Solution {
    public void sortColors(int[] nums) {
        if (nums == null || nums.length == 0) return;

        int left = 0;
        int right = nums.length - 1;

        while(left < nums.length && nums[left] == 0) {
            left++;
        }

        while(right >= 0 && nums[right] == 2) {
            right--;
        }    

        int i = left;

        ...
  }
  ```

```java
    public void sortColors(int[] nums) {

这里要求one pass完成排序，需要利用只有数组元素只有3个数的特性，否则无法完成。排序完成后一定是0...01...12....2，所以可以扫描数组，当遇到0时，交换到前部，当遇到1时，交换到后部。用双指针left, right来记录当前已经就位的0序列和2序列的边界位置。

假设已经完成到如下所示的状态：

0......0   1......1  x1 x2 .... xm   2.....2
           |          |         |
           left      cur     right

(1) A[cur] = 1：已经就位，cur++即可
(2) A[cur] = 0：交换A[cur]和A[left]。由于A[left]=1或left=cur，所以交换以后A[cur]已经就位，cur++，left++
(3) A[cur] = 2：交换A[cur]和A[right]，right--。由于xm的值未知(1或0)，cur不能增加，继续判断xm。

    if(nums == null || nums.length == 0)  
    return;
    int left = 0;
    int right = nums.length - 1;
    int i = 0;
    while (i <= right) {
        if (nums[i] == 0) {
            swap(nums, left, i);
            left++;
            i++;
        } else if (nums[i] == 1) {
            i++;
        } else if (nums[i] == 2) {
            swap(nums, right, i);
            right--;
        }
    }
    }

    private void swap (int[] nums, int a, int b) {
        int temp = nums[a];
        nums[a] = nums[b];
        nums[b] = temp;
    }
```

[Sort Colors II](http://www.lintcode.com/en/problem/sort-colors-ii/)

```java
class Solution {
    /**
     * @param colors: A list of integer
     * @param k: An integer
     * @return: nothing
     */
    public void sortColors2(int[] colors, int k) {
        // write your code here
        if (colors == null || colors.length == 0) return;
        
        rainbowSort(colors, 0, colors.length - 1, 1, k);
    }
    
    //sort the colors between index start-> end, colors range are from colorFrom to colorTo
    private void rainbowSort(int[] colors, int start, int end, int colorFrom, int colorTo) {
        if (start >= end) return;
        
        if (colorFrom >= colorTo) return;
        
        int colorMid = colorFrom + (colorTo - colorFrom) / 2;
        
        int left = start;
        int right = end;
        while (i <= j) {
            //为了保证left -> right 包含全部的colorMid，要把所有midColor全部放在左边
            while (left <= right && colors[left] <= colorMid) {
                left++;
            }
            
            while (left <= right && colors[right] > colorMid) {
                right--;
            }
            
            if (left <= right) {
                swap(colors, left, right);
                left++;
                right--;
            }
        }
        
        rainbowSort(colors, start, right, colorFrom, colorMid);
        rainbowSort(colors, left, end, colorMid + 1, colorTo);
    }
    
    private void swap(int[] colors, int a, int b) {
        int tmp = colors[a];
        colors[a] = colors[b];
        colors[b] = tmp;
    }
}
```



