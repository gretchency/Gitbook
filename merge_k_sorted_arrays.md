# Merge K Sorted Arrays

```java
public class MergeKArrays {
    public static int[] mergeK(List<int[]> lists) {
        if (lists == null || lists.size() == 0) return null;
        
        return mergeSort(lists, 0, lists.size() - 1);
    }
    
    public static int[] mergeSort(List<int[]> lists, int start, int end) {
        if(start == end) {
            return lists.get(start);
        }
        int mid = start + (end - start) / 2;
        int[] left = mergeSort(lists, start, mid);
        int[] right = mergeSort(lists, mid + 1, end);
        return merge(left, right);
    }
    public static int[] merge(int[] list1, int[] list2) {
        int[] merged = new int[list1.length + list2.length];
        int i = 0;
        int j = 0;
        int index = 0;
        while (i < list1.length && j <list2.length) {
            if (list1[i] < list2[j]) {
                merged[index++] = list1[i++];
            } else {
                merged[index++] = list2[j++];
            }
        }
        
        if (i < list1.length) {
            for (int k = i; k < list1.length; k++) {
                merged[index] = list1[k];
            }
        }
        
        if (j < list2.length) {
            for (int k = j; k < list2.length; k++) {
                merged[index] = list2[j];
            }
        }
        
        return merged;
    }
```