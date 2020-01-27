go [back](DP-MENU.md)

# __Bellman-Ford algorithm__

## __Introduction__

* Let **G = (V, E)** be a directed graph 
* Assume that each edge **(i, j)** in E has a weight **c<sub>ij</sub>**
* When computing shortest paths in graphs one would think of **Dijkstra's algorithm**, however, that algorithm fails when the edges in the graph have negative weights

* If **G** has no negative cycles, then there is a shortest path from **s** to **t** that is simple(does not repeat nodes), and hence has at most n - 1 edges

* Let **opt(i, v)** denote the minimum cost of a v-t path using at most i edges. Therefore, we seek to find **opt(n - 1, s)** 

* We need to find an optimal path **P** representing **opt(i, v)**:
    * If the path uses at most **i - 1** edges, then **opt(i, v) = opt(i - 1, v)**
    * If the path uses **i** edges, and the first edge is **(v, w)**, then **opt(i, v) = c<sub>vw</sub> + opt(i - 1, w)**`
* Leads to this recursive formula: If i > 0 then
**opt(i, v) = min(opt(i - 1, v), min<sub>w in V</sub>(opt(i - 1, v) + c<sub>vw</sub>))**

## __Implementation__
 
pseudocode: 
```java
int getShortestPath(int n, int s, int t) {
    int[][] opt = new int[n][n];

    for (int i = 0; i < n; i++) {
        opt[0][i] = Integer.MAX_VALUE;
    }

    opt[0][t] = 0;

    for (int i = 1; i <= n - 1; i++) {
        for v in V { 
            //compute opt[i][v] using above recurrence
        }
    }

    return opt[n - 1][s];
}
```

## __Analysis__

* Time complexity: O(**n<sup>3</sup>**) in any graph that has no negative cycles
* Space complexity: O(**n<sup>2</sup>**)


  

