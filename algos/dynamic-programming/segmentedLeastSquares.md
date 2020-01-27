go [back](DP-MENU.md)

# __Segmented least squares__

## __Introduction__

* Given a set of points **P = {(x<sub>1</sub>, y<sub>1</sub>), (x<sub>2</sub>, y<sub>2</sub>), ..., (x<sub>n</sub>, y<sub>n</sub>)}** with **x<sub>1</sub> < x<sub>2</sub> < ... < x<sub>n</sub>**
* Often when looking at scientific or statistical data, plotted on a twodimensional set of axes, </br> one tries to pass a “line of best fit” through the
data
* Thus, we need a problem formulation that requires us to fit the points well, using as few lines as possible
* Suppose **opt(i)** denotes the optimum solution for the points **p<sub>1</sub>, p<sub>2</sub>, ..., p<sub>i</sub>** and **e<sub>i, j</sub>** = minimum error of any line with respect to  **p<sub>i</sub>, p<sub>i+1</sub>, ..., p<sub>j</sub>**

* If last segment of optimal partition is **p<sub>i</sub>, p<sub>i+1</sub>, ..., p<sub>n</sub>**, then **opt(n) = e<sub>i, n</sub> + C + opt(i - 1)**
* **C** represents a fixed given multiplier greater than 0

* We have the following recurrence for points **p<sub>i</sub>, p<sub>i+1</sub>, ..., p<sub>j</sub>**: 
    * **opt(j) = min(e<sub>i, j</sub> + C + opt(i - 1))**, where min is taken over 1 <= i <= j

## __Implementation__
 
pseudocode:
```java
int SegmentedLeastSquares(int n) {
    int[] opt = new int[n + 1];

    for all pairs i <= j
        Compute error i, j FOR segment pi...pj;
    endfor

    for j = 1, 2 ... n 
        opt[j] = min(error i,j + C + opt(i - 1));
    endfor

    return opt[n];
}
```

## __Analysis__

* Time complexity: O(**n<sup>3</sup>**), but can be improved to O(**n<sup>2</sup>**)
* Space complexity: O(**n<sup>2</sup>**) - because we store the error for each **e<sub>i, j</sub>**


  

