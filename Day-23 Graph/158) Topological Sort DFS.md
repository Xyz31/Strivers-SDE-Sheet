# Topological Sort DFS


```md



```
 
# Approach - I
```cpp

/*
    Time complexity: O(V+E)
    Space complexity: O(V)
    
    Where V is the number of vertices and E is the number of edges.
*/

#include <stack>

void topologicalSortUtil(vector<vector<int>> &adj, vector<bool> &visited, stack<int> &stk, int src) {
    // Mark current vertex visited
    visited[src] = true;  

    // Iterating over adjacent vertices.
    for(int node : adj[src]) {
        if(!visited[node]) {
            topologicalSortUtil(adj, visited, stk, node);
        }
    }
    // Push vertex in stack after pushing all its adjacent (and their adjacent and so on) verices.
    stk.push(src);
}

vector<int> topologicalSort(vector<vector<int>> &edges, int v, int e) {
    // Creating adjacency list.
    vector<vector<int>> adj(v);
    for(int i = 0; i < e; i++) {
        adj[edges[i][0]].push_back(edges[i][1]);
    } 

    vector<bool> visited(v);
    stack<int> stk;

    // Recursively finding topological sorting.
    for(int i = 0; i < v; i++) {
        if(!visited[i]) {
            topologicalSortUtil(adj, visited, stk, i);
        }
    }

    // vector 'result' will keep topological sort of given graph.
    vector<int> result;
    while(!stk.empty()) {
        result.push_back(stk.top());
        stk.pop();
    }

    return result;
}

```


# Approach - II Kahn's Algo
```cpp

/*
    Time complexity: O(V+E)
    Space complexity: O(V)
    
    Where V is the number of vertices and E is the number of edges.
*/

#include <queue>

vector<int> topologicalSort(vector<vector<int>> &edges, int v, int e) {
    // Creating adjacency list.
    vector<vector<int>> adj(v);
    for(int i = 0; i < e; i++) {
        adj[edges[i][0]].push_back(edges[i][1]);
    } 
    // Calculaing indegree of each vertex.
    vector<int> indegree(v);
    for(auto edge : edges) {
        indegree[edge[1]]++;
    }
    // Push all vertices of indegree 0 in queue.
    queue<int> que;
    for(int i = 0; i < v; i++) {
        if(indegree[i] == 0) {
            que.push(i);
        }
    }
    vector<int> result; // It will store topological sort of the given graph.
    // Finding topologial sorting
    while(!que.empty()) {
        int src = que.front();
        que.pop();
        result.push_back(src);
        for(int node : adj[src]) {
            indegree[node]--;
            if(indegree[node] == 0) {
                que.push(node);
            }
        }
    }
    return result;
}

```