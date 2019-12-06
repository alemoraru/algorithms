go [back](GREEDY-MENU.md)
# Union Find

The <b><i>Union-Find</i></b> (also known as <b><i>Disjoint-Set</i></b>) data structure can track elements
partitioned into disjoint subsets. It provides near-constant time operations merge
(<b><i>union</i></b>) and contains (<b><i>find</i></b>) operations.

## Operations

There are 3 types of operations in a **Union-Find** data structure:
* **MakeSet(n)** which creates *n* initial sets, all containing 1 element.
* **Find(x)** which returns the id of the set that x is in
* **Union(x, y)**, which merges the sets that *x* and *y* are in.

## Implementation

* Union-Find class composition

```java 
class UnionFind {

    private int[] parent;
    private int[] rank;

    // Union Find structure implemented 
    // with two arrays for Union by Rank
    // Constructor is makeSet(n) operation
    public UnionFind(int size) {

        // parents array, initialised first with i,
        parent = new int[size];  for each node i

        // ranks array, initialised first with 0
        rank = new int[size]; 

        for (int i = 0; i < size; i++) {
            parent[i] = i; // parent of its own
        }
    }
}
```

* **Find(x)** operation, which finds the parent of the subset in which the given node is 

```java
 /**
   * this function should does path compression
   * @param i index of a node
   * @return the root of the subtree containg i.
   */
  int find(int i) {
    if (this.parent[i] != i) {
      this.parent[i] = find(this.parent[i]);
    }
    
    return parent[i];
  }
```

* **Union(x, y)** which merges the 2 subsets of the 2 given nodes

```java
  /**
   * Merge two subtrees if they have a different parent, input is array indices
   * @param i a node in the first subtree
   * @param j a node in the second subtree
   * @return true iff i and j had different parents.
   */
  boolean union(int i, int j) {

    int xSet = this.find(i);
    int ySet = this.find(j);
    
    // check if two nodes belong or not to the same subtree
    // if no, then check their rank and keep as parent the one with 
    // highest rank; in case of equality keep either one as parent 
    // and increment by 1 the rank of that node
    if (xSet == ySet) {
      return false;
    } else if (rank[xSet] < rank[ySet]) {
      parent[xSet] = ySet;
    } else {
      parent[ySet] = xSet;
      if (rank[ySet] == xSet) {
        rank[xSet] ++;
      }
    }
    return true;
  }
```
## Complexity 

* MakeSet(n) is **O(n)**
* Find is **O(log n)**
* Union is **O(log n)**

## Applications 

* Can be used for efficient cycle detection in an undirected graph, therefore it is used when applying **Kruskal's algorithm** for determining a **Mininimum Spanning Tree(MST)**