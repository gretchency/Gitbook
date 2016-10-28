# Three Sum

http://www.lintcode.com/en/problem/3sum/

二刷的坑
* 先sort
* for loop 的length - 2
* 跳过重复
* 找到一个sum后，```left++```, ```right--``` 此时两个while判断是否重复, ```right``` 和 ```right + 1```比


Sort 整个array

先确定一个数 然后从后面找两个数 三个数之和为0

找后俩数的时候用两个指针一前一后往中间走

sum < 0 说明多往前走一个

sum > 0 说明多往后走一个

**注意如果相同数字要规避掉节省时间
**

*和2sum做法完全不同。用递归＋回溯会超时。正确做法是排序，然后先取一个数，剩下两个用双指针，小了就左指针右移，大了就右指针左移。O(n^2)的复杂度。递归回溯应该是n选3，所以是O(n^3), 这个不是很确定，如果有错请指出。*



O(n^2)时间复杂度

```java
public class Solution {
    /**
     * @param numbers : Give an array numbers of n integer
     * @return : Find all unique triplets in the array which gives the sum of zero.
     */
    public ArrayList<ArrayList<Integer>> threeSum(int[] numbers) {
        // write your code here
        
        ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>>();
        
        if (numbers == null || numbers.length < 3) {
            return res;
        }
        
        //先sort 再用两个指针
        Arrays.sort(numbers);
        
        for (int i = 0; i < numbers.length - 2; i++) {
            //避免重复的list
            if (i > 0 && numbers[i] == numbers[i - 1]) continue;
            int left = i + 1;
            int right = numbers.length - 1;
            
            while(left < right) {
                
                int sum = numbers[i] + numbers[left] + numbers[right];
                if (sum == 0) {
                    ArrayList<Integer> tmp = new ArrayList<Integer>();
                    tmp.add(numbers[i]);
                    tmp.add(numbers[left]);
                    tmp.add(numbers[right]);
                    res.add(tmp);
                    left++;
                    right--;
                    
                    //跳过重复
                    while (left < right && numbers[left] == numbers[left - 1]) {
                        left++;
                    }
                    
                    //跳过重复 注意这里right + 1
                    while (left < right && numbers[right] == numbers[right + 1]) {
                        right--;
                    }
                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
            
        }
        
        return res;
    }
}
```

HashSet + 2Sum
```java
public class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();

        if (nums == null || nums.length < 3) return res;
        
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i++) {
            if (i > 0 && nums[i - 1] == nums[i]) continue;
            int target = 0 - nums[i];
            
            //Map<Integer, Integer> map = new HashMap<>();
            Set<Integer> set = new HashSet<>();
            
            for (int j = i + 1; j < nums.length; j++) {
                if (j > 1 && nums[j - 1] == nums[j]) continue;
                int num = target - nums[j];
                if (set.contains(num)) {
                    List<Integer> list = new ArrayList<>();
                    list.add(nums[i]);
                    list.add(num);
                    list.add(nums[j]);
                    res.add(list);
                } else {
                    set.add(nums[j]);
                }
            }
        }
        
        return res;
    }
}
```

Follow UP:

4Sum:
* 和3Sum的思路一样，在计算4Sum时我们可以先选一个数，然后在剩下的数中计算3Sum。而计算3Sum则同样是先选一个数，然后再剩下的数中计算2Sum
*一样一样的，只是三重循环也是注意去重

3Sum Closest
* 维护与target差值最小的sum，每次比一下差多少，比原sum小就更新

```java
public class Solution {
    public int threeSumClosest(int[] nums, int target) {
        if (nums == null || nums.length < 3) return Integer.MIN_VALUE;
        
        Arrays.sort(nums);
        int min = nums[0] + nums[1] + nums[2];

        for (int i = 0; i < nums.length - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            
            int left = i + 1;
            int right = nums.length - 1;
            
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (Math.abs(sum - target) < Math.abs(min - target)) {
                    min = sum;
                }
                if (sum == target) return sum;
                if (sum > target) right--;
                if (sum < target) left++;
            }
        }
        
        return min;
    }
}
```