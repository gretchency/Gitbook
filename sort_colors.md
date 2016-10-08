# Sort Colors

左右指针记录边界

二刷

```java
        while(left < nums.length && nums[left] == 0) {
            left++;
        }

        while(right >= 0 && nums[right] == 2) {
            right--;
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
(3) A[cur] = 2：交换A[cur]和A[right]，right--。由于xm的值未知，cur不能增加，继续判断xm。
    
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