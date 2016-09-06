# Three Sum

http://www.lintcode.com/en/problem/3sum/

Sort 整个array

先确定一个数 然后从后面找两个数 三个数之和为0

找后俩数的时候用两个指针一前一后往中间走

sum < 0 说明多往前走一个

sum > 0 说明多往后走一个

**注意如果相同数字要规避掉节省时间
**

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