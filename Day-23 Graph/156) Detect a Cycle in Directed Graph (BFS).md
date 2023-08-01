# Detect a Cycle in Directed Graph(BFS) | Topological Sort | Kahn’s Algorithm


# Approach - I
```cpp

/*
    Time Complexity: O(N+M)
    Space Complexity: O(N)
    
    Where N is the number of nodes and M is the number of edges in the given graph.
*/

#include <list>

#include <queue>

class Graph {
    int noOfNodes;

    // Pointer to an array containing adjacency lists.
    list < int > * adj;

    public:
        // Act as Constructor.
        Graph(int noOfNodes);

    // To add an edge to between two nodes in a Graph.
    void addEdge(int v, int w);

    // Returns true if there exists a cycle in the given graph.
    bool checkCyclic();
};

Graph::Graph(int noOfNodes) {
    this -> noOfNodes = noOfNodes;
    adj = new list < int > [noOfNodes];
}

void Graph::addEdge(int a, int b) {
    adj[a].push_back(b);
}

bool Graph::checkCyclic() {
    /* 
      Create a vector to store indegrees 
      (number of incoming edges)
      of all vertices and initialize all indegrees as 0.
    */
    vector < int > inDegree(noOfNodes, 0);

    // Traverse adjacency lists to fill indegrees of vertices.
    for (int u = 0; u < noOfNodes; u++) {
        for (auto v: adj[u]) {
            inDegree[v]++;
        }
    }

    // Create an queue and enqueue all vertices with indegree 0.
    queue < int > zeroInDegreeQ;

    for (int i = 0; i < noOfNodes; i++) {
        if (inDegree[i] == 0) {
            zeroInDegreeQ.push(i);
        }
    }

    // Initialize count of visited nodes.
    int cnt = 0;

    // Create a vector to store result (Topological Ordering).
    vector < int > topoOrdering;

    /*
      One by one dequeue vertices from queue and 
      enqueue adjacents if indegree of adjacent becomes 0.
    */

    while (zeroInDegreeQ.empty() == false) {
        // Extract front of queue and add it to topological order.
        int u = zeroInDegreeQ.front();
        zeroInDegreeQ.pop();
        topoOrdering.push_back(u);

        /*
          Iterate through all its neighbouring nodes of 
          dequeued node and decrease their number of 
          incoming edges by 1.
        */

        list < int > ::iterator itr;

        for (itr = adj[u].begin(); itr != adj[u].end(); itr++) {
            /* 
                If the number of incoming edges becomes zero 
                then add it to the queue.
            */
            if (--inDegree[ * itr] == 0) {
                zeroInDegreeQ.push( * itr);
            }
        }

        cnt++;
    }

    // Check if there exists a cycle.
    if (cnt != noOfNodes) {
        return true;
    } else {
        return false;
    }
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


