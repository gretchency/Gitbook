# Binary Search 整合

**Search Insert Position** [leet](https://leetcode.com/problems/search-insert-position/)
* find first position that value is >= target

**Search a 2D Matrix** [leet](https://leetcode.com/problems/search-a-2d-matrix/)
* matrix[mid / col][mid % col] == target
* Search a 2D Matrix II: left bottom to top right

**First Position of Target**
```java
if (nums[mid] == target)
                //cannot return, cuz it may not be the first position
                end = mid;
```

**Search in a big Sorted Array** [leet](https://adambillylee.gitbooks.io/lintcode/content/chapter2.3.html)

```java
// find an end to start with
    while(reader.get(end) != -1 && reader.get(end)<target) {
        end = end * 2 + 1;
    }
```

Find Minimum in Rotated Sorted Array
* find first position <= the last number

**Search in Rotated Sorted Array**
* 注意截取的时候 ```target >= nums[start] && target <= nums[mid]``` 才能保证在那一小段里

**Find Peak Element**
* 砍掉一半的方法
* 根据题意，该数组必定至少存在一个peak,由此可知若A[mid - 1] > A[mid],peak在mid左半边，A[mid] < A[mid + 1],peak在右半边，由此可求得Peak.

**Search for a Range**
* 两次二分，找first position和last postion