# Sorting

MergeSort

* void函数里不能直接A = mergeSort(A)

When you pass array to this method, you **pass it by value** - that is, you make a brand new variable that ALSO points to the same object. If you edit the variable array in your method to point to a new array, it doesn't also make the other variable point to your new array - it still points to the old array. So when you return you haven't done any edits to the array that was passed in.



```java
public void sortIntegers2(int[] A) {
        // Write your code here
        int[] B = mergeSort(A);
        for (int i = 0; i < A.length; i++) {
            A[i] = B[i];
        }
        //A = B.clone();
        //
    }
    
    public int[] mergeSort(int[] unsorted) {
        if (unsorted.length <= 1) {
            return unsorted;
        }
        
        int mid = unsorted.length / 2;
        int[] left = new int[mid];
        System.arraycopy(unsorted, 0, left, 0, mid);
        int[] right = new int[unsorted.length - mid];
        System.arraycopy(unsorted, mid, right, 0, unsorted.length - mid);
        
        left = mergeSort(left);
        right = mergeSort(right);
        
        return merge(left, right);
    }
    
    public int[] merge(int[] left, int[] right) {
        int indexLeft = 0;
        int indexRight = 0;
        int index = 0;
        
        int[] merged = new int[left.length + right.length];
        while (indexLeft < left.length && indexRight < right.length) {
            if (left[indexLeft] < right[indexRight]) {
                merged[index] = left[indexLeft];
                indexLeft++;
            } else {
                merged[index] = right[indexRight];
                indexRight++;
            }
            index++;
        }
        
        if (indexLeft < left.length) {
            for (int i = indexLeft; i < left.length; i++) {
                merged[index++] = left[i];
            }
        } else {
            for (int i = indexRight; i < right.length; i++) {
                merged[index++] = right[i];
            }
        }
        
        return merged;
    }
```


Quick Sort

i, j各自移不动的时候swap, 终止条件i <= j

```java
    private void quickSort(int[] A, int left, int right) {
        if (left >= right) {
            return;
        }

        // partition
        //int pivot = A[left + (right - left) / 2];
        int pivot = A[right];
        int i = left, j = right;
        while (i <= j) {
            while (i <= j && A[i] < pivot) {
                i++;
            }
            while (i <= j && A[j] > pivot) {
                j--;
            }

            if (i <= j) {
                swap(A, i, j);
                i++;
                j--;
            }
        }

        quickSort(A, left, j);
        quickSort(A, i, right);
    }
```