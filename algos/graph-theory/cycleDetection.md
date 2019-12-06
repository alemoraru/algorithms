go [back](GRAPHS-MENU.md)
# Graph Theory *1

## Cycle detection in a directed graph

* Given a directed graph, check whether the graph contains a cycle or not. Your function should return true if the given graph contains at least one cycle, else return false. For example, the following graph contains three cycles 0->2->0, 0->1->2->0 and 3->3,so your function must return true.

* Depth First Traversal can be used to detect a cycle in a Graph. DFS for a connected graph produces a tree. There is a cycle in a graph only if there is a back edge present in the graph. A back edge is an edge that is from a node to itself (self-loop) or one of its ancestor in the tree produced by DFS. 

```c++
// A C++ Program to detect cycle in a graph 
#include<iostream> 
#include <list> 
#include <limits.h> 
  
using namespace std; 
  
class Graph 
{ 
    int V;    // No. of vertices 
    list<int> *adj;    // Pointer to an array containing adjacency lists 
    bool isCyclicUtil(int v, bool visited[], bool *rs);  // used by isCyclic() 
public: 
    Graph(int V);   // Constructor 
    void addEdge(int v, int w);   // to add an edge to graph 
    bool isCyclic();    // returns true if there is a cycle in this graph 
}; 
  
Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 
} 
  
void Graph::addEdge(int v, int w) 
{ 
    adj[v].push_back(w); // Add w to v’s list. 
} 
  
//utility recursive function for detecting a cycle
bool Graph::isCyclicUtil(int v, bool visited[], bool *recStack) 
{ 
    if(visited[v] == false) 
    { 
        // Mark the current node as visited and part of recursion stack 
        visited[v] = true; 
        recStack[v] = true; 
  
        // Recur for all the vertices adjacent to this vertex 
        list<int>::iterator i; 
        for(i = adj[v].begin(); i != adj[v].end(); ++i) 
        { 
            if ( !visited[*i] && isCyclicUtil(*i, visited, recStack) ) 
                return true; 
            else if (recStack[*i]) 
                return true; 
        } 
  
    } 
    recStack[v] = false;  // remove the vertex from recursion stack 
    return false; 
} 
  
// Returns true if the graph contains a cycle, else false. 
bool Graph::isCyclic() 
{ 
    // Mark all the vertices as not visited and not part of recursion 
    // stack 
    bool *visited = new bool[V]; 
    bool *recStack = new bool[V]; 
    for(int i = 0; i < V; i++) 
    { 
        visited[i] = false; 
        recStack[i] = false; 
    } 
  
    // Call the recursive helper function to detect cycle in different 
    // DFS trees 
    for(int i = 0; i < V; i++) 
        if (isCyclicUtil(i, visited, recStack)) 
            return true; 
  
    return false; 
}
```

A java equivalent fucntion would be like this: 

```java
// A Java Program to detect cycle in a graph 
import java.util.ArrayList; 
import java.util.LinkedList; 
import java.util.List; 
  
class Graph { 
      
    private final int V; 
    private final List<List<Integer>> adj; 
  
    public Graph(int V)  
    { 
        this.V = V; 
        adj = new ArrayList<>(V); 
          
        for (int i = 0; i < V; i++) 
            adj.add(new LinkedList<>()); 
    } 
      
    // Utility recursive function for detecting a cycle
    private boolean isCyclicUtil(int i, boolean[] visited, 
                                      boolean[] recStack)  
    { 
          
        // Mark the current node as visited and 
        // part of recursion stack 
        if (recStack[i]) 
            return true; 
  
        if (visited[i]) 
            return false; 
              
        visited[i] = true; 
  
        recStack[i] = true; 
        List<Integer> children = adj.get(i); 
          
        for (Integer c: children) 
            if (isCyclicUtil(c, visited, recStack)) 
                return true; 
                  
        recStack[i] = false; 
  
        return false; 
    } 
  
    private void addEdge(int source, int dest) { 
        adj.get(source).add(dest); 
    } 
  
    // Returns true if the graph contains a  
    // cycle, else false. 
    private boolean isCyclic()  
    { 
          
        // Mark all the vertices as not visited and 
        // not part of recursion stack 
        boolean[] visited = new boolean[V]; 
        boolean[] recStack = new boolean[V]; 
          
          
        // Call the recursive helper function to 
        // detect cycle in different DFS trees 
        for (int i = 0; i < V; i++) 
            if (isCyclicUtil(i, visited, recStack)) 
                return true; 
  
        return false; 
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
        Graph graph = new Graph(4); 
        graph.addEdge(0, 1); 
        graph.addEdge(0, 2); 
        graph.addEdge(1, 2); 
        graph.addEdge(2, 0); 
        graph.addEdge(2, 3); 
        graph.addEdge(3, 3); 
          
        if(graph.isCyclic()) 
            System.out.println("Graph contains cycle"); 
        else
            System.out.println("Graph doesn't "
                                    + "contain cycle"); 
    } 
} 
```

## Iterative approach of cycle detection in a directed graph

The iterative approach makes use of a stack where we have a DFS-similar like structure. Instead of using the above mentiones ```isCylicRec```, we simply swap its usage with the ```isCycleIt```.


```java
//iterative cycle detection helper function
    private boolean isCyclicIt(int i, boolean[] visited, boolean[] recStack) {

        // Mark the current node as visited and
        // part of recursion stack
        //and check base cases
        if (recStack[i])
            return true;

        if (visited[i])
            return false;

        visited[i] = true;
        recStack[i] = true;

        Stack<Integer> stack = new Stack<>();

        stack.push(i);

        while (!stack.isEmpty()) {
            Integer curr = stack.peek();

            if(!visited[curr]) {
                visited[curr] = true;
                recStack[curr] = true;
            } else {
                recStack[curr] = false;
                stack.pop();
            }

            //get children of current node
            List<Integer> children = adj.get(curr);
            for (Integer adj : children) {
                if (!visited[adj]) {
                    stack.push(adj);
                } else if (recStack[adj]) {
                    return true;
                }
            }
        }
        return false;
    }
```

