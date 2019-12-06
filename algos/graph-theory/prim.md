# Prim's algorithm for minimum spanning tree

Given a weighted, undirected graph <i>__G__</i> with __n__ vertices and __m__ edges. You want to find a spanning tree of this graph which connects all vertices and has the least weight (i.e. the sum of weights of edges is minimal). A spanning tree is a set of edges such that any vertex can reach any other by exactly one simple path. The spanning tree with the least weight is called a minimum spanning tree.

__Note:__ 

* It is easy to see that any spanning tree will necessarily contain <i>__n−1__</i> edges.

* This problem appears quite naturally in a lot of problems. For instance in the following problem: there are n cities and for each pair of cities we are given the cost to build a road between them (or we know that is physically impossible to build a road between them). We have to build roads, such that we can get from each city to every other city, and the cost for building all roads is minimal.

## Implementation for dense graphs __<i>O(n<sup>2</sup>)</i>__

__<u>Approach</u>__

* We approach this problem for a different side: for every not yet selected vertex we will store the minimum edge to an already selected vertex.

* Then during a step we only have to look at these minimum weight edges, which will have a complexity of __<i>O(n)</i>__.

* After adding an edge some minimum edge pointers have to be recalculated. Note that the weights only can decrease, i.e. the minimal weight edge of every not yet selected vertex might stay the same, or it will be updated by an edge to the newly selected vertex. Therefore this phase can also be done in __<i>O(n)</i>__.

* Thus we received a version of Prim's algorithm with the complexity __<i>O(n<sup>2</sup>)</i>__.


__<u>Implementation</u>__


```c++
int n;
vector<vector<int>> adj; // adjacency matrix of graph
const int INF = 1000000000; // weight INF means there is no edge

struct Edge {
    int w = INF, to = -1; //w - weight & to - "outgoing" node
};

void prim() {
    int total_weight = 0;
    vector<bool> selected(n, false); //visited vector
    vector<Edge> min_e(n); //for min spanning tree
    min_e[0].w = 0;

    for (int i = 0; i < n; ++i) {
        int v = -1;
        for (int j = 0; j < n; ++j) {
            if (!selected[j] && (v == -1 || min_e[j].w < min_e[v].w))
                v = j;
        }

        if (min_e[v].w == INF) {
            cout << "No MST!" << endl;
            exit(0);
        }

        selected[v] = true;
        total_weight += min_e[v].w;
        if (min_e[v].to != -1)
            cout << v << " " << min_e[v].to << endl;

        for (int to = 0; to < n; ++to) {
            if (adj[v][to] < min_e[to].w)
                min_e[to] = {adj[v][to], v};
        }
    }

    cout << total_weight << endl;
}
```

## Implementation for sparse graphs __<i>O(m </i>log <i>n)</i>__

__Note:__ For sparse graphs this is better than the above algorithm, but for dense graphs this will be slower.

```c++
const int INF = 1000000000;

struct Edge {
    int w = INF, to = -1;
    //redefine comparison operator
    bool operator<(Edge const& other) const {
        return w < other.w;
    }
};

int n;
vector<vector<Edge>> adj;

void prim() {
    int total_weight = 0;
    vector<Edge> min_e(n);
    min_e[0].w = 0;
    set<Edge> q;
    q.insert({0, 0});
    vector<bool> selected(n, false);
    for (int i = 0; i < n; ++i) {
        if (q.empty()) {
            cout << "No MST!" << endl;
            exit(0);
        }

        int v = q.begin()->to;
        selected[v] = true;
        total_weight += q.begin()->w;
        q.erase(q.begin());

        if (min_e[v].to != -1)
            cout << v << " " << min_e[v].to << endl;

        for (Edge e : adj[v]) {
            if (!selected[e.to] && e.w < min_e[e.to].w) {
                q.erase({min_e[e.to].w, e.to});
                min_e[e.to] = {e.w, v};
                q.insert({e.w, e.to});
            }
        }
    }

    cout << total_weight << endl;
}
```

__<u>Algorithm notes</u>__

* Here the graph is represented via a adjacency list __adj[]__, where __adj[v]__ contains all edges (in form of weight and target pairs) for the vertex __v__. 
* __min_e[v]__ will store the weight of the smallest edge from vertex __v__ to an already selected vertex (again in the form of a weight and target pair). In addition the queue __q__ is filled with all not yet selected vertices in the order of increasing weights __min_e__. 
* The algorithm does __n__ steps, on each of which it selects the vertex __v__ with the smallest weight __min_e__ (by extracting it from the beginning of the queue), and then looks through all the edges from this vertex and updates the values in __min_e__ (during an update we also need to also remove the old edge from the queue __q__ and put in the new edge).

