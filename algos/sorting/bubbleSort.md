go [back](SORTING-MENU.md)
# Bubble Sort

This sorting algorithm revolves around the idea of checking each element with the next and swapping when in wrong order. Essentially, this algorithm is really slow, therefore other sorting algorithms are recommended, such as  **merge sort** or **quick sort**.

## Algorithm

```java 
public static void bubbleSort(int[] arr ) {
    for (int i = 0; i < arr.length; i++) {
        for (int j = i + 1; j < arr.length; j++) {
            if (arr[i] > arr[j]) {
                int aux = arr[i];
                arr[i] = arr[j];
                arr[j] = aux;
            }
        }
    }
}

public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);

    int n = sc.nextInt();
    int[] arr  = new int[n];

    for (int i = 0; i < n; i++) {
        arr[i] = sc.nextInt();
    }
    
    bubbleSort(arr); // apply selection sort
    sc.close();
}
```

## Complexity

* **Time complexity** of Selection Sort is O(**n<sup>2</sup>**)
* **Space complexity**: O(**1**) </br>
* **In place?**: Yes
* **Stable?**: Yes

