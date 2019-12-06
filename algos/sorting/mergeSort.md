go [back](SORTING-MENU.md)
# Merge Sort

Like QuickSort, Merge Sort is a **Divide and Conquer** algorithm. It divides input array in two halves, calls itself for the two halves and then merges the two sorted halves. The **merge()** function is used for merging two halves. The **merge(arr, l, m, r)** is key process that assumes that arr[l..m] and arr[m+1..r] are sorted and merges the two sorted sub-arrays into one.

## Algorithm 

```java
private static void merge(int[] arr, int l, int m, int r) {
        int n1 = m - l + 1; // size of left array
        int n2 = r - m; // size of right array 

        // initialize left & right arrays
        int[] left = new int[n1]; 
        int[] right = new int[n2];

        int k = 0;

        // put all elements left of element 
        // at index m in left array (including m)
        for (int i = 0; i < n1; i++) {
            left[i] = arr[l + i];
        }

        // put all elements right of element 
        // at index m in right array (excluding m)
        for (int j = 0; j < n2; j++) {
            right[j] = arr[m + 1 + j];
        }
        k = l;

        int i = 0, j = 0;

        // for each element check iteratively which 
        // current element is smaller (either from left or 
        // from right array)
        while (i < n1 && j < n2) {
            if (left[i] <= right[j]) {
                arr[k++] = left[i++];
            } else {
                arr[k++] = right[j++];
            }
        }

        // if there are any elements left
        // in any of the 2 arrays
        while (i < n1) {
            arr[k++] = left[i++];
        }

        while (j < n2) {
            arr[k++] = right[j++];
        }
    }
```
* The recursive calls are performed in the "mergeSort" method
* As long as the **l** is smaller than **r**, then you can 
continue to split the array even more

```java
private static void mergeSort(int[] arr, int l, int r) {
        if (l < r) {
            int m = (l + r) / 2;

            mergeSort(arr, l, m);
            mergeSort(arr, m + 1, r);

            merge(arr, l, m, r);
        }
    }
```

Example of a driver function for reading array and applying merge sort.

```java
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int[] arr  = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }

        mergeSort(arr, 0, arr.length - 1); // apply merge sort
        sc.close();
    }
```
## Complexity

* **Time complexity** of Merge Sort is O(**n log n**) in all 3 cases (worst, average and best) as merge sort always divides the array into two halves and take linear time to merge two halves
* **Space complexity**: O(**n**)
* **In place?**: Not in a typical implementation
* **Stable?**: Yes
