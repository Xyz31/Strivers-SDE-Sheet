# Detect a Cycle in Directed Graph(DFS) | Topological Sort | Kahn’s Algorithm


```md



```
 
# Approach - I
```cpp

/*
    Time Complexity: O(N+M)
    Space Complexity: O(N)
    
    Where N is the number of nodes and M is the number of edges in the given graph.
*/

#include <list>

class Graph {
    int noOfNodes;

    // Pointer to an array containing adjacency lists.
    list < int > * adj;

    // Helper function for checkCyclic().
    bool checkCyclicHelper(int v, vector < bool > & checkVisited, vector < bool > & rStack);

    public:
        // Act as Constructor.
        Graph(int noOfNodes);

    // To add an edge to between two nodes in a Graph.
    void addEdge(int a, int b);

    // Returns true if there exists a cycle in the given graph.
    bool checkCyclic();
};

Graph::Graph(int noOfNodes) {
    this -> noOfNodes = noOfNodes;
    adj = new list < int > [noOfNodes];
}

void Graph::addEdge(int a, int b) {
    // Add b to a's list.
    adj[a].push_back(b);
}

bool Graph::checkCyclicHelper(int v, vector < bool > & checkVisited, vector < bool > & rStack) {

    if (checkVisited[v] == false) {
        /* 
            Make the current node as visited
            and part of recursion stack.
        */
        checkVisited[v] = true;
        rStack[v] = true;

        // Recur for all the nodes adjacent to this node.
        list < int > ::iterator i;

        for (i = adj[v].begin(); i != adj[v].end(); ++i) {
            if (!checkVisited[ * i] && checkCyclicHelper( * i, checkVisited, rStack)) {
                return true;
            } else if (rStack[ * i]) {
                return true;
            }
        }
    }

    // Remove the vertex from recursion stack.
    rStack[v] = false;

    return false;
}

bool Graph::checkCyclic() {
    /* 
        Initialise checkVisited as false 
        i.e. nodes are not visited yet.
    */
    vector < bool > checkVisited(noOfNodes, false);

    // Initialise nodes as not a part of recursion stack.
    vector < bool > rStack(noOfNodes, false);

    /* 
        Call the recursive helper function 
        to detect cycle in different DFS trees.
    */

    for (int i = 0; i < noOfNodes; i++) {
        if (checkCyclicHelper(i, checkVisited, rStack)) {
            return true;
        }
    }
    return false;
}

int detectCycleInDirectedGraph(int n, vector < pair < int, int >> & edges) {
    Graph directedG(n);

    int m = edges.size();

    for (int i = 0; i < m; i++) {
        directedG.addEdge(edges[i].first - 1, edges[i].second - 1);
    }

    return directedG.checkCyclic();
}

```

