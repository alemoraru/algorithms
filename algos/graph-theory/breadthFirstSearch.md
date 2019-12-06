go [back](GRAPHS-MENU.md)
# __Breadth First Search (BFS)__

## __Introduction__
* Breadth first search is one of the basic and essential searching algorithms on graphs.

* As a result of how the algorithm works, the path found by breadth first search to any node is the shortest path to that node, i.e the path that contains the smallest number of edges in unweighted graphs.

* The algorithm works in O(*__n__* + *__m__*) time, where *__n__* is number of vertices and *__m__* is the number of edges.

# __Implementation(Iterative)__ 

c++ implementation: 
```c++

    int N; //number of nodes
    int s; //source vertex

    vector<int> adj[N]; //adjacency list representation 
    queue<int> q; //used for bfs
    vector<bool> used(n); //array of visited vertices

    q.push(s); //push starting vertex 
    used[s] = true; //and mark it as visited

    while(!q.empty()) {
        int v = q.front();
        cout << v << " "; //output current vertex
        q.pop();
        for (u : adj[v]) {
            if (!used[u]) {
                used[u] = true;
                q.push(u);
            }   
        }
    }
``` 
or in java: 

```java 
/**
    * Breadth first search performed in a iterative approach
    * @param adj - adjacency list for given graph
    * @param visited - array marking nodes that were already visited or not
    * @param source - source node to start traversal from
    */
public static void bfs(ArrayList<ArrayList<Integer>> adj, boolean[] visited, int source) {
    Queue<Integer> que = new LinkedList<>(); // data structure used for bfs
    que.add(source); // add starting vertex to queue
    visited[source] = true; // mark starting vertex as being visited

    while (!que.isEmpty()) {
        int v = que.poll();

        System.out.println(v + " ");
        for (Integer u : adj.get(v)) {
            if (!visited[u]) {
                que.add(u);
                visited[u] = true;
            }
        }
    }
}
```

# __Implementation(Recursive)__ 

c++ implementation: 
```c++

``` 
or in java: 

```java 

```


*WIP