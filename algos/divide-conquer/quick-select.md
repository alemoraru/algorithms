# Quick select

**Quickselect** is a selection algorithm to find the **kth smallest** element in an unordered list. It is related to the **quicksort** sorting algorithm.

## Algorithm 

* **partition** method
```java
 public static int partition(int[] arr, int l, int r) {
    int pivot = arr[r]; // take last element as pivot to compare to 
    int pivotLoc = l; 

    // start from leftmost index and count how many
    // elements are smaller than pivot. If smaller, 
    // swap with pivotLoc position and increment pivotLoc pointer
    for (int i = l; i <= r; i++) {
      if (arr[i] < pivot) {
        int aux = arr[i];
        arr[i] = arr[pivotLoc];
        arr[pivotLoc] = aux;
        
        pivotLoc++;
      }
    }
    
    // after elements are to the left of pivot
    // put pivot in the right position
    int aux = arr[r];
    arr[r] = arr[pivotLoc];
    arr[pivotLoc] = aux;
    
    return pivotLoc;
  }
```

* **quickSelect** method
```java
public static int quickSelect(int[] arr, int l, int r, int index) {
    int partition = partition(arr, l, r);

    // if partition same index that means kth smallest 
    // element is at the partition position    
    if (partition == index) {
      return arr[partition];
    }
    
    // if partition greater than index, then take only first half of the array
    // otherwise take right half of the array
    if (partition > index) {
      return quickSelect(arr, l, partition - 1, index);
    } else {
      return quickSelect(arr, partition + 1, r, index);
    }
  }
```

## Complexity

* Has a worst-case time complexity of O(**n<sup>2</sup>**)
* Can be improved to **linear tine** if implemented via **median of medians** method