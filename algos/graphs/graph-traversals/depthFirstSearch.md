# __Depth First Search (DFS)__

## __Introduction__
* Depth First Search is one of the main graph algorithms.

* Depth First Search finds the lexicographical first path in the graph from a source vertex *__u__* to each vertex. Depth First Search will also find the shortest paths in a tree (because there only exists one simple path), but on general graphs this is not the case.

* The algorithm works in O(*__n__* + *__m__*) time, where *__n__* is number of vertices and *__m__* is the number of edges.

# __Implementation__

```c++

    int N; //number of nodes
    int s; //source vertex

    vector<int> adj[N]; //adjacency list representation 
    stack<int> q; //used for dfs
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