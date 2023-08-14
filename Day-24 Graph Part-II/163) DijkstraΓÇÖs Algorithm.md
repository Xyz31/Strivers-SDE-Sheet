# DijkstraΓÇÖs Algorithm


```md



```
 
# Approach - I Using The Adjacency Matrix.
```cpp

/*
    Time complexity: O(V^2)
    Space complexity: O(V^2)

    Where â€˜Vâ€™ is the number of vertices in a graph.
*/

// Finds the vertex with minimum distance.
int minDistance(vector<int> distance, vector<bool> visited, int vertices) {
    int min = INT_MAX, minVertex;
    
    for (int v = 0; v < vertices; v++) {
        if (visited[v] == false && distance[v] <= min) {
            min = distance[v];
            minVertex = v;
        }
    }
    return minVertex;
}

vector<int> dijkstraHelper(vector<vector<int>> &matrix, int vertices, int source) {
    vector<int> distance(vertices, INT_MAX);
    vector<bool> visited(vertices, false);

    // Distance of source to itself is 0.
    distance[source] = 0;

    for(int i = 0; i < vertices; i++){

        int u = minDistance(distance, visited, vertices);

        // Mark the current vertex as visied.
        visited[u] = true;
        
        // Update the distances of the adjacent nodes.
        for (int v = 0; v < vertices; v++) {
            if (!visited[v] && matrix[u][v] && distance[u] != INT_MAX && distance[u] + matrix[u][v] < distance[v]) {
                distance[v] = distance[u] + matrix[u][v];
            }
        }
    }
    return distance;
}

vector<int> dijkstra(vector<vector<int>> &vec, int vertices, int edges, int source) {
    vector< vector<int>> matrix(vertices, vector<int>(vertices,0));

    // Create an adjacency matrix from the given input.F
    for (int i = 0; i < vec.size(); i++) {
        int u = vec[i][0];
        int v = vec[i][1];
        int w = vec[i][2];
        if(matrix[u][v]!=0){
            matrix[u][v]=min(matrix[u][v],w);
            matrix[v][u]=min(matrix[v][u],w);
        }
        else{
            matrix[u][v]=w;
            matrix[v][u]=w;
        }
    }
    return dijkstraHelper(matrix, vertices, source);
}

```


# Approach - II Using The Adjacency List.
```cpp

/*
    Time complexity: O(E*log(V))
    Space complexity: O(V^2)

    Where 'E' is the number of edges and 'V' is
    the number of vertices in a graph.
*/

vector<int> dijkstraHelper(vector<vector<pair<int, int>>> &adjacencyList, int vertices, int source) {

    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    vector<int> distance(vertices, INT_MAX);

    // Push the source vertex in the priority queue.
    pq.push({0, source});

    // Distance of a vertex to itself is 0.
    distance[source] = 0;
    vector<bool> visited(vertices, false);

    // Loop till all vertices are visited.
    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();
        visited[u] = true;

        // Update the distances of the adjacent nodes.
        for (auto it = adjacencyList[u].begin(); it != adjacencyList[u].end(); it++) {
            int v = it -> first;
            int dist = it -> second;

            if (visited[v] == false && distance[v] > distance[u] + dist) {
                distance[v] = distance[u] + dist;
                pq.push({distance[v], v});
            }
        }
    }
    return distance;
}
vector<int> dijkstra(vector<vector<int>> &vec, int vertices, int edges, int source) {
    
    vector<vector<pair<int, int>>> adjacencyList(vertices);

    // Create an adjacency list.
    for (int i = 0; i < (int)vec.size(); i++) {
        
        adjacencyList[vec[i][0]].push_back({vec[i][1], vec[i][2]});
        adjacencyList[vec[i][1]].push_back({vec[i][0], vec[i][2]});
    }
    return dijkstraHelper(adjacencyList, vertices, 0);
}


```