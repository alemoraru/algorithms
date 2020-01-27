go [back](DP-MENU.md)

# __Sequence Alignment__

## __Introduction__

* Given **X**, **Y** - 2 strings of length **m** and **n** respectively, find an **alignment** of these 2 strings such that the cost is minimized, that is, find a _matching_ **M** of the sets X, Y
* A _mathcing_ **M** is considered an **alignment** if there are no "crossing pairs" : if (i, j) , (i', j') are in M and i < i', **then** j < j'
* Suppose M is given an alignment between **X** and **Y**:
    * First, &delta; > 0 defines a gap penalty
    * Second, &alpha;<sub>pq</sub> defines a mismatch for lining up p with q, thus for each (i, j) in M we pay cost 
    &alpha;<sub>x<sub>i</sub>y<sub>j</sub></sub> for lining up x<sub>i</sub> with y<sub>j</sub>. 
    * &alpha;<sub>pp</sub> = 0 for each letter p
    * cost of M is the sum of its gaps and mismatch costs and we seek an alignment of minimum costs

* **opt(i, j)** = min cost for aligning sequence **x<sub>1</sub>x<sub>2</sub>...x<sub>i</sub>** and **y<sub>1</sub>y<sub>2</sub>...y<sub>j</sub>**

* If M is an optimal alignment, at least one of the following is true: 
    1. (m, n) is in M
    2. the m<sup>th</sup> position of X is not matched
    3. the n<sup>th</sup> position of Y is not matched
    </br></br>
    * if 1. holds we pay &alpha;<sub>x<sub>m</sub>y<sub>n</sub></sub> and then align **x<sub>1</sub>x<sub>2</sub>...x<sub>m - 1</sub>** with **y<sub>1</sub>y<sub>2</sub>...y<sub>n - 1</sub>**. </br>
    Therefore we get **opt(m, n)** = &alpha;<sub>x<sub>m</sub>y<sub>n</sub></sub> + opt(m - 1, n - 1)
    * if 2. holds we pay gap &delta; </br>
    Therefore we get **opt(m, n)** = &delta; + opt(m - 1, n)
    * if 3. holds we pay gap &delta; </br>
    Therefore we get **opt(m, n)** = &delta; + opt(m, n - 1)

* The minimum cost for aligning i >= 1 and j >= 1 is </br>
**opt(i, j) = min[&alpha;<sub>x<sub>i</sub>y<sub>j</sub></sub> + opt(i - 1, j - 1), &delta; + opt(i - 1, j), &delta; + opt(i, j - 1)]**

* opt(i, 0) = opt(0, i) = i * &delta; for all i, since the only way of aligning an i-letter word with a 0-letter word is to use i gaps

## __Implementation__

```java
public static int getMinAlignment(String firstString, String secondString) {
    // get length of both strings
    int m = firstString.length(), n = secondString.length(); 
    
    // initialize memoization array
    int[][] mem = new int[m + 1][n + 1]; 
    
    // create the gaps for aligning an i-letter word 
    // with a 0-letter word. If a penalty gap would be 
    // provided then mem[i][0] = gap * i
    for (int i = 1; i <= m; i++) {
      mem[i][0] = i;
    }
    
    // analogous with previous statement
    for (int j = 1; j <= n; j++) {
      mem[0][j] = j;
    }
    
    for (int i = 1; i <= m; i++) {
      for (int j = 1; j <= n; j++) {
        // here the mismatch is 1, however it could provided or computed beforehand as something else
        // here we use the recurrence mentioned in the introduction
        int mismatch = compare(firstString.charAt(i - 1), secondString.charAt(j - 1));
        mem[i][j] = Math.min(mismatch + mem[i - 1][j - 1], Math.min(1 + mem[i - 1][j], 1 + mem[i][j - 1]));
      }
    }
    
    return mem[m][n];
}

// as mentioned before, the mismatch here is considered
// 1 when characters don't match and 0 otherwise. However, 
// penalty could be different
public static int compare(char x, char y) {
    return x != y ? 1 : 0
}
```

## Analysis

* Time complexity: O(**n * m**)
* Space complexity: O(**n * m**)


  

