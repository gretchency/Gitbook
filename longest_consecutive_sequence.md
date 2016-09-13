# Longest Consecutive Sequence

Given [100, 4, 200, 1, 3, 2],
The longest consecutive elements sequence is [1, 2, 3, 4]. Return its length: 4.


Longest Consecutive Sequence: 从无序的数列中找出最长的连续数列的长度，用O(n)时间。这种很诡异的时间限制基本就要想到hashmap, 这道用hashset就能做，因为只要存一个value。全存到hashset以后遍历hashset里的值，分别往左往右找，找到连续的值就删，因为包含一个特定数的序列只有一个（仔细体会）。找不到了就返回序列长度。

```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return an integer
     */
    public int longestConsecutive(int[] num) {
        // write you code here
        HashSet<Integer> set = new HashSet<>();
        
        for (int n: num) {
            set.add(n);
        }
        
        int longest = 0;
        
        for (int i = 0; i < num.length; i++) {
            //向左看
            int down = num[i] - 1;
            int count = 1;
            while (set.contains(down)) {
                //先remove掉，因为序列唯一
                set.remove(down);
                down--;
                count++;
            }
            
            //向右看
            int up = num[i] + 1;
            while (set.contains(up)) {
                set.remove(up);
                up++;
                count++;
            }
            
            longest = Math.max(longest, count);
        }
        
        return longest;
    }
}
```