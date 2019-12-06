go [back](GRAPHS-MENU.md)
# Dijkstra's Algorithm

You are given a directed or undirected weighted graph with __n__ vertices and __m__ edges. The weights of all edges are non-negative. You are also given a starting vertex __s__. This article discusses finding the lengths of the shortest paths from a starting vertex s to all other vertices, and output the shortest paths themselves

This problem is also called __single-source shortest paths problem__.

## Algorithm

Let's create an array __d[]__ where for each vertex v we store the current length of the shortest path from __s__ to __v__ in __d[v]__. Initially __d[s]=0__, and for all other vertices this length equals infinity. In the implementation a sufficiently large number (which is guaranteed to be greater than any possible path length) is chosen as infinity.
    
* __d[v] = inf__, where v != s

In addition, we maintain a boolean array u[], which stores for each vertex v wheter it's marked. Initially all vertices are unmarked.

* __u[v] = false__

## Implementation

Dijkstra's algorithm performs n iterations. On each iteration it selects an unmarked vertex v with the lowest value d[v], marks it and checks all the edges (v,to) attempting to improve the value d[to].

* __Complexity__ : O(n<sup>2</sup> + m) 

This algorithm is optimal for dense graph, when m ~ n<sup>2</sup>.
However, in sparse graphs, when __m__ is much smaller than the maximal number of edges n<sup>2</sup>, the problem can be solved in O(n log n + m) complexity.

```c++
const int INF = 1000000000;
vector<vector<pair<int, int>>> adj;

void dijkstra(int s, vector<int> & d, vector<int> & p) {
    int n = adj.size();
    d.assign(n, INF);
    p.assign(n, -1);
    vector<bool> u(n, false);

    d[s] = 0;
    for (int i = 0; i < n; i++) {
        int v = -1;
        for (int j = 0; j < n; j++) {
            if (!u[j] && (v == -1 || d[j] < d[v]))
                v = j;
        }

        if (d[v] == INF)
            break;

        u[v] = true;
        for (auto edge : adj[v]) {
            int to = edge.first;
            int len = edge.second;

            if (d[v] + len < d[to]) {
                d[to] = d[v] + len;
                p[to] = v;
            }
        }
    }
}
```

## Dijkstra with better complexity 

```c++
const int INF = 1000000000;
vector<vector<pair<int, int>>> adj;

void dijkstra(int s, vector<int> & d, vector<int> & p) {
    int n = adj.size();
    d.assign(n, INF);
    p.assign(n, -1);

    d[s] = 0;
    set<pair<int, int>> q;
    q.insert({0, s});
    while (!q.empty()) {
        int v = q.begin()->second;
        q.erase(q.begin());

        for (auto edge : adj[v]) {
            int to = edge.first;
            int len = edge.second;

            if (d[v] + len < d[to]) {
                q.erase({d[to], to});
                d[to] = d[v] + len;
                p[to] = v;
                q.insert({d[to], to});
            }
        }
    }
}
```

or its java counterpart:

```java

//helper Pair class
class Pair {
    int to;
    int len;

    Pair(int to, int len) {
        this.to = to;
        this.len = len;
    }
}

ArrayList<ArrayList<Pair>> adj;

private void dijkstra(int s, int[] d, int[] p) {
        int n = d.length;

        Arrays.fill(d, Integer.MAX_VALUE);
        Arrays.fill(p, -1);

        d[s] = 0;

        Queue<Pair> q = new LinkedList<>();
        q.add(new Pair(0, s));

        while (!q.isEmpty()) {
            int v = q.poll().to;

            for (Pair edge : adj.get(v)) {
                int to = edge.to;
                double len = edge.len;

                if (d[v] + len < d[to]) {
                    d[to] = d[v] + len;
                    p[to] = v;
                
                    q.add(new Pair(to, d[to]));
                }
            }
        }
    }
```

__*WIP__