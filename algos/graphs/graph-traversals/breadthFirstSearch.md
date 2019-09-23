# __Breadth First Search (BFS)__

## __Introduction__
* Breadth first search is one of the basic and essential searching algorithms on graphs.

* As a result of how the algorithm works, the path found by breadth first search to any node is the shortest path to that node, i.e the path that contains the smallest number of edges in unweighted graphs.

* The algorithm works in O(*__n__* + *__m__*) time, where *__n__* is number of vertices and *__m__* is the number of edges.

# __Implementation__

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

*WIP