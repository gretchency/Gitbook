# Sorting

* Stable: Bubble, Insertion, MergeSort
* Non-Stable: Selection, QuickSort

MergeSort

* void函数里不能直接A = mergeSort\(A\), main函数里的A其实没有改变

When you pass array to this method, you **pass it by value** - that is, you make a brand new variable that ALSO points to the same object. If you edit the variable array in your method to point to a new array, it doesn't also make the other variable point to your new array - it still points to the old array. So when you return you haven't done any edits to the array that was passed in.

```java
   public void sortIntegers(int[] A) {
        // Write your code here
        int[] B = sort(A);
        for (int i = 0; i < A.length; i++) {
            A[i] = B[i];
        }
    }

    public static int[] sort(int[] A) {
        if (A.length <= 1) {
            return A;
        }
        return mergeSort(A, 0, A.length - 1);
    }

    public static int[] mergeSort(int[] A, int start, int end) {
        //BASE CASE不能忘！
        if (start == end) return new int[]{A[start]};

        int mid = start + (end - start) / 2;
        int[] left = mergeSort(A, start, mid);
        int[] right = mergeSort(A, mid + 1, end);

        return merge(left, right);
    }

    public static int[] merge(int[] left, int[] right) {
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

i, j各自移不动的时候swap, 终止条件i &lt;= j

**Worst Case: Pivot选的不好，每次选了最小的数或者最大的数，这样到最后只排好一个数，有n个数所以有n层，每层都要处理n个数，时间复杂度O\(n^2\)**

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

```java
//Bubble
//两两比较，大的往上bubble up,最后最大的排最后
public void bubbleSort(int[] A) {
    //outer从最后一位开始，直到比到只剩1个数
    for (int outer = A.length - 1; outer >= 1; outer--) {
        //比好的bubble up 到最后了，只比没比好的
        for (int in = 0； in < out; in++) {
            //两两比较
            if (A[in] > A[in + 1]) {
                //内部不断swap
                swap(A, in, in + 1);
            }
        }
    }
}

//Selection
//每一轮将最小的放最前面
public void selectSort(int[] A) {
    for (int outer = 0; outer < A.length - 1; outer++) {
        //min记录当前最小值
        int min = outer;
        //比好的在最前，只比没比好的
        for(int in = outer + 1; in < A.length; in++) {
            if (A[min] > A[in]) {
                min = in;
            }
        }
        swap(A,outer, min);
    }
}

//Insertion
//把要比的作为tmp先放到外面，然后把比他大的都往右挪，给他腾位置，最后插入tmp
public void insertionSort(int[] A) {
    for (int outer = 1; outer < A.length; outer++) {
        int tmp = A[outer];
        int in = outer;
        while (in > 0 && A[in - 1] > tmp) {
            A[in] = A[in - 1];
            in--;
        }

        if (in != outer) {
            A[in] = tmp;
        }
    }
}
```



