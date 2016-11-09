# Intersection of Two Arrays

```
Given two arrays, write a function to compute their intersection.

Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].

Each element in the result must be unique.
The result can be in any order.
```

1.两个Set,第一个set存第一个array的元素，然后看第二个array里元素在不在第一个set里，在的话加入第二个set. 最后遍历set输出
```java
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();
        Set<Integer> interSet = new HashSet<>();
        for (int num: nums1) {
            set.add(num);
        }
        
        for (int num: nums2) {
            if (set.contains(num)) {
                interSet.add(num);
            }
        }
        
        int[] res = new int[interSet.size()];
        int index = 0;
        for (Integer i: interSet) {
            res[index++] = i;
        }
        return res;
        
    }
}
```