go [back](SORTING-MENU.md)
# Insertion Sort
* Insertion sort is a simple sorting algorithm that works the way we sort playing cards in our hands. 
* For each iteration of the array, we take a key as the current element and shift all elements 1 position backwards while they are greater than the key.

## Algorithm

```java 
public static void insertionSort(int[] arr) {
        for (int i = 1; i < arr.length; i++) {
            int key = arr[i];
            int j = i - 1;

            /* Move elements of arr[0..i-1], that are
               greater than key, to one position ahead
               of their current position */
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = key;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int[] arr  = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }
        
        insertionSort(arr); // apply insertion sort
        sc.close();
    }
```
## Complexity

* **Time complexity** of Selection Sort is O(**n<sup>2</sup>**)
* **Space complexity**: O(**1**) </br>
* **In place?**: Yes
* **Stable?**: Yes