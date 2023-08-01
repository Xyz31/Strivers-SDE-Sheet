# Detect Cycle in an Undirected Graph (using BFS)


# Approach - I
```cpp

/*
    Time Complexity : O(N + M)
    Space Complexity : O(N)

    where 'N' is the number of vertices and
    'M' is the number of edges in the graph.
*/

#include <queue>

bool isCycle (int vertex, vector<vector<int>>& graph, vector<bool>& visited, vector<int>& parent)
{
    visited[vertex] = true;

    queue<int> q;

    q.push(vertex);

    while(q.size()!=0)
    {
        int remVertex = q.front();
        q.pop();

        for(int adjVertex : graph[remVertex])
        {
            if (visited[adjVertex] == false)
            {
                visited[adjVertex] = true;
                q.push(adjVertex);
                parent[adjVertex] = remVertex;
            }

            else if (visited[adjVertex] == true && parent[remVertex] != adjVertex)
            {
                return true;
            }
        }
    }
    return false;
}

string cycleDetection (vector<vector<int>>& edges, int n, int m)
{
    vector<vector<int>> graph(n + 1, vector<int>());

    for (int i = 0; i < m; i++)
    {
        graph[edges[i][1]].push_back(edges[i][0]);
        graph[edges[i][0]].push_back(edges[i][1]);
    }

    vector<bool> visited(n + 1, false);
    vector<int> parent(n + 1, -1);

    for (int i = 1; i <= n; i++)
    {
        if (visited[i] == false)
        {
            if (isCycle (i, graph, visited, parent) == true)
            {
                return "Yes";
            }
        }
    }

    return "No";
}



```


# Approach - II Union Find
```cpp

/*
    Time Complexity : O(M * log(N))
    Space Complexity : O(N)

    where 'N' is the number of vertices and
    'M' is the number of edges in the graph.
*/

int findparent (int i, vector<int>& parent)
{
    if (i == parent[i])
    {
        return i;
    }
    return parent[i] = findparent (parent[i], parent);
}

string cycleDetection (vector<vector<int>>& edges, int n, int m)
{
    vector<int> parent(n + 1, 0);
    vector<int> rank(n + 1, 0);

    for (int i = 1; i <= n; i++)
    {
        rank[i] = 1;
        parent[i] = i;
    }

    for (vector<int>& ar : edges)
    {
        int u = ar[0];
        int v = ar[1];

        int p1 = findparent (u, parent);
        int p2 = findparent (v, parent);

        if (p1 != p2)
        {
            if (rank[p1] < rank[p2])
            {
                parent[p1] = p2;
            }
            else if (rank[p1] > rank[p1])
            {
                parent[p2] = p1;
            }
            else
            {
                parent[p1] = p2;
                rank[p2]++;
            }
        }
        else
        {
            return "Yes";
        }
    }
    
    return "No";
}


```