go [back](DP-MENU.md)

# __RNA secondary structure__

## __Introduction__

* {A, C, G, T} - the four basic units of DNA
* A-T & C-G - base pairings
* View a single-stranded RNA molecule as a sequence of n symbols(bases) drawn from {A, C, G, U} 
* **B = b<sub>1</sub>b<sub>2</sub>...b<sub>n</sub>** where any b<sub>i</sub> is in {A, C, G, U}
* We say a secondary structure on B is a set of pairs **S = {(i, j)}**, where i, j in {1, 2, ..., n} that satisfies:
    1. No sharp turns: Ends of each pair in S separated by at least 4 bases: if (i, j) in S, then **i < j - 4**
    2. Only {A, U} and {C, G} can be paired in either order
    3. S is a matching: no base appears in more than one pair 
    4. Non-crossing condition: if (i, j) and (k, l) are 2 pairs in S, then we can't have i < k < j < l

* Let **opt(i, j)** denote max number of base pairings in a secondary structure on **b<sub>i</sub>b<sub>i+1</sub>...b<sub>j</sub>**
* **opt(i, j) = 0** whenever i >= j - 4
* For **b<sub>i</sub>b<sub>i+1</sub>...b<sub>j</sub>**:
    * **j** is not involved in a pair
    * **j** is involved in a pair with some **t < j - 4**
* Let **&theta;** denote the optimal solution:
    * if **j** isn't in **&theta;**, then **opt(i, j) = opt(i, j - 1)**
    * if **j** is in **&theta;**, then we recur on **opt(i, t - 1)** and **opt(t + 1, j - 1)**

* we have recurrence: **opt(i, j) = max(opt(i, j - 1), max(1 + opt(i, t - 1) + opt(t + 1, j - 1)))**

## __Implementation__
 
pseudocode:
```java
int getMaxNumberOfPairings() {
    //Initialize opt(i, j) = 0, whenever i >= j - 4

    for (int k = 5; k <= n - 1; k++) {
        for (int i = 1; i <= n - k; i++) {
            int j = i + k;
            // compute opt(i, j) with above recurrence
        }
    }

    return opt[1][n];
}
```

## __Analysis__

* Time complexity: O(**n<sup>3</sup>**)
* Space complexity: O(**n<sup>2</sup>**)


  

