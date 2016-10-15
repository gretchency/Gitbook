# Two Sum

HashMap O(n)时空

http://www.lintcode.com/en/problem/two-sum/#

A + B = target  B = target - A

* map的key是与target的差值，也就是需要的第二个数，value是当前index
* 注意返回值不是0-based 所以放进map的时候要i + 1

```java
public int[] twoSum(int[] numbers, int target) {
        // write your code here
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        if (numbers.length < 2) {
            return null;
        }
        
        for (int i = 0; i < numbers.length; i++) {
            int second = target - numbers[i];
            if (map.containsKey(second)) {
                int[] result = {map.get(second), i + 1}; 
                return result;
            } else {
                map.put(numbers[i], i+1);
            }
        }
        
        
        return null;
    
    }
```
