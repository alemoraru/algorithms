go [back](DP-MENU.md)

# __Subset sums & Knapsack problem__

## __Introduction__

* We use **opt(i, w)** to denote the value of the optimal solution using a subset of items **{1, ..., i}** </br>
and a maximum allowed weight **w**
* **opt(i, w)** = max<sub>S</sub> &#931;<sub>j in S</sub>(w<sub>j</sub>), where maximum is over subsets S including {1, ..., i} that satisfy w<sub>j</sub> <= w

* we want **opt(n, W)**

* let &theta; denote the optimal solution:
    * if n doesn't belong to &theta;, then **opt(n, W) = opt(n - 1, W)** (we ignore item n)
    * if n belongs to &theta;, then **opt(n, W) = w<sub>n</sub> + opt(n - 1, W - w<sub>n</sub>)**

* Therefore, the recurrence equation is given by: 
    * if w < w<sub>i</sub>, then **opt(i, w) = opt(i - 1, w)**
    * else, **opt(i, w) = max(opt(i - 1, w), w<sub>i</sub> + opt(i - 1, w - w<sub>i</sub>))**

* **Subset sums** is a special case for the **Knapsack problem**. In the Knapsack problem we have an array of values and there we seek to maximize the total value while using as much weight as possible, therefore the recurrence is given by: 
    * If n doesn't belong to &theta;, then **opt(n, w) = opt(n - 1, w)**
    * If n belongs to &theta;, then **opt(n, w) = max(opt(i - 1, w), v<sub>i</sub> + opt(i - 1, w - w<sub>i</sub>))**

* The implementation for both is fairly similar and therefore I will provide the one for the **Knapsack problem**

## __Implementation__

For Knapsack: 

```java
public static int findMaxSum(int n, int W, int[] weights, int[] values) {
    int[][] opt = new int[n + 1][W + 1];

    // both weights and values array start from  
    // position 1 and end at position n
    // weights[0] and values[0] should be ignored

    for (int i = 1; i <= n; i++) {
      for (int w = 1; w <= W; w++) {
        if (w < weights[i]) {
          opt[i][w] = opt[i - 1][w];
        } else {
          opt[i][w] = Math.max(opt[i - 1][w], values[i] + opt[i - 1][w - weights[i]]);
        }
      }
    }

    return opt[n][W];
}

```
## __Analysis__

* Time complexity: O(**n * W**), where W is total allowed weight
* Space complexity:  O(**n * W**)


  

