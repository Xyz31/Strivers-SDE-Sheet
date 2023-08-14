# Strongly Connected Components – Kosaraju’s Algorithm

```md



```
 

# Approach - I
```cpp

/*
    Time Complexity: O(V + E)
    Space Complexity: O(V)

    Where V is the number of vertices,
    E is the number of edges in the graph.
*/

#include <stack>

// This marks the discovery time of the nodes
int discoveryTime = 1;

// DFS to visit all the nodes in linear time
void dfs(vector<vector<int>> &graph, int node, vector<int> &disc, vector<int> &low, vector<bool> &inStack, stack<int> &nodeStack, vector<vector<int>> &ans)
{
    disc[node] = discoveryTime;
    low[node] = discoveryTime;

    ++discoveryTime;

    nodeStack.push(node);
    inStack[node] = true;

    // Using Tarjan's algorithm here
    for (int v : graph[node])
    {
        // Visiting all unvisited nodes
        if (disc[v] == -1)
        {
            dfs(graph, v, disc, low, inStack, nodeStack, ans);
            low[node] = min(low[node], low[v]);
        }
        else if (inStack[v])
        {
            low[node] = min(low[node], disc[v]);
        }
    }

    // If current node is root of a SCC
    if (low[node] == disc[node])
    {
        // component stores one of the possible SCCs
        vector<int> component;
        int u;
        while (nodeStack.top() != node)
        {
            u = nodeStack.top();
            nodeStack.pop();
            inStack[u] = false;

            component.push_back(u);
        }

        u = nodeStack.top();
        nodeStack.pop();
        inStack[u] = false;

        component.push_back(u);
        // Inserting the current SCC into the answer
        ans.push_back(component);
    }
}

vector<vector<int>> stronglyConnectedComponents(int n, vector<vector<int>> &edges)
{
    // This stores our graph as Adjacency list
    vector<vector<int>> graph(n);

    for (vector<int> &edge : edges)
    {
        graph[edge[0]].push_back(edge[1]);
    }

    // Arrays to store the low-link value and discovery time of the nodes
    vector<int> disc(n, -1);
    vector<int> low(n, -1);

    stack<int> nodeStack;
    vector<bool> inStack(n, false);

    vector<vector<int>> ans;
    for (int i = 0; i < n; i++)
    {
        if (disc[i] == -1)
        {
            // Node 'i' has not been visited.
            dfs(graph, i, disc, low, inStack, nodeStack, ans);
        }
    }

    // Return the final answer
    return ans;
}

```


