# Majority Number

naive:

map过一遍

```java
public class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        
        for (int num: nums) {
            if (!map.containsKey(num)) {
                map.put(num, 1);
            } else {
                map.put(num, map.get(num) + 1);
            }
            
            if (map.get(num) > nums.length / 2) return num;
        }
        
        return 0;
    }
}
```

中阶：
* 搞一个计数器，让每一个数和其他数pk，还是他就计数器++,不是他就计数器--,最后看还存活下来的数是谁
* O(n) , O(1)

```java
public class Solution {
    public int majorityElement(int[] nums) {
        int key = -1;
        int count = 0;
        
        for (int num: nums) {
            if (count == 0) {
                key = num;
                count = 1;
                continue;
            } 
            
            if (key == num) {
                count++;
            } else {
                count--;
            }
            
            
        }
        
        return key;
    }
}
```