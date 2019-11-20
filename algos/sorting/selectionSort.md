# Selection Sort

* The selection sort algorithm sorts an array by repeatedly finding the **minimum element** (considering ascending order) from unsorted part and putting it at the beginning. The algorithm maintains two subarrays in a given array.
* In every iteration of selection sort, the **minimum element** (considering ascending order) from the unsorted subarray is picked and moved to the sorted subarray.

## Algorithm

```java
public static void selectionSort(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            
            // index of smallest element  
            // in current sub array
            int min_index = i; 
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[j] < arr[i]) {
                    min_index = j;
                }
            }

            // swap the smallest element 
            // with current i element
            int aux = arr[i];
            arr[i] = arr[min_index];
            arr[min_index] = aux;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int[] arr  = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }
        selectionSort(arr); // apply selection sort
        sc.close();
    }
```
## Complexity

* **Time complexity** of Selection Sort is O(**n<sup>2</sup>**) as there are two nested loops.
* **Space complexity**: O(**1**) </br>
The good thing about selection sort is it never makes more than O(**n**) swaps and can be useful when memory write is a costly operation.
* **In place?**: Yes, it does not require extra space. 
* **Stable?**: The default implementation is not stable. However it can be made stable
    