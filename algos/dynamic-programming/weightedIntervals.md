go [back](DP-MENU.md)

# __Weigthed interval scheduling__

## __Introduction__

* We are given n intervals(requests) each with a start time, finish time, and a weight or value
* The idea is to sort the requests in order of non-decreasing finish time such that </br>
f<sub>1</sub> <= f<sub>2</sub> <= ... <= f<sub>n</sub>
* We will say a request i comes before j if i < j
* Also we define an array p where **p(j)** = largest index i < j such that f<sub>i</sub> <= s<sub>j</sub>, </br> where f<sub>i</sub> denotes finish time of request i and s<sub>j</sub> denotes start time of request j

* we define **opt(j) = max(v<sub>j</sub> + opt(p(j)), opt(j - 1))** </br> 
therefore request j belongs to an optimal solution on the set {1, 2, ..., j} if and only if v<sub>j</sub> + opt(p(j)) >= opt(j - 1)

## __Implementation__

Find predecessors implementation: 

```java
public static int[] findPredecessors(int n, int[] s, int[] f) {
    int[] p = new int[n + 1];
    Arrays.fill(p, -1);
    
    for (int i = 1; i <= n; i++) {
      p[i] = binarySearch(1, n, s[i], f);
    }
    
    return p;
}

public static int binarySearch(int low, int high, int[] f, int si) {
    int mid = (low + high) / 2;
    
    if (low > high) {
      return high == 0 ? -1 : high;
    }
    
    if (finish[mid] > si) {
      return binarySearch(low, mid - 1, si);
    } else {
      return binarySearch(mid + 1, high, si);
    }
  }
```
Getting the maximum value for optimal scheduling: 

```java
public static int solve(int n, int[] s, int[] f, int[] v, int[] p) {
    int[] opt = new int[n + 1];
  
    for (int i = 1; i <= n; i++) {
      int job = p[i] < 0 ? 0 : opt[p[i]];
      
      opt[i] = Math.max(v[i] + job, opt[i - 1]);
    }

    return opt[n];
  }
```

code snippet to get the optimal solution: 
```java
while (i >= 1) {
      int job = p[i] < 0 ? 0 : opt[p[i]];
      
      if (v[i] + job >= opt[i - 1]) {
        // ith job was used for the optimal solution
        // so we print the index of that job  
        System.out.print(i + " ");
        i = p[i];
      } else {
        i--;
      }
    }
```

## __Analysis__

* Time complexity: O(**n * log n**) - since we perform a bynary search </br> for each element when computing its predecessor
* Space complexity: O(**n**)


  

