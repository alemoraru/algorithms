go [back](SORTING-MENU.md)
# Quick Sort

Like **Merge Sort**, **QuickSort** is a **Divide and Conquer** algorithm. It picks an element as **pivot** and partitions the given array around the picked pivot. There are many different versions of quickSort that pick pivot in different ways :

* Always pick **first** element as pivot.
* Always pick **last** element as pivot (implemented below)
* Pick a **random** element as pivot.
* Pick **median** as pivot.

## Algorithm

```java
public static int partition(int[] arr, int low, int high) {
        int pivot = arr[high]; // take pivot as last element
        int i = low;

        for (int j = low; j < high; j++) {

            // check all elements smaller than pivot
            if (arr[j] < pivot) {
                int aux = arr[i];
                arr[i] = arr[j];
                arr[j] = aux;

                i++;
            }
        }

        // move pivot to correct postion
        // after checking all elements in 
        // current partition
        int aux = arr[i];
        arr[i] = arr[high];
        arr[high] = aux;

        return i;
    }
    public static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int partition = partition(arr, low, high);

            quickSort(arr, low, partition - 1);
            quickSort(arr, partition + 1, high);
        }
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int[] arr  = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }
        
        quickSort(arr, 0, arr.length - 1); // apply quick sort
        
        sc.close();
    }
```
## Complexity

* Worst-case time complexity is O(**n<sup>2</sup>**), which can happen if we are always choosing lowest/highest element/
* We can get a O(**n log n**) worst-case time complexity when we partition around the **median** element, since finding it takes linear time.