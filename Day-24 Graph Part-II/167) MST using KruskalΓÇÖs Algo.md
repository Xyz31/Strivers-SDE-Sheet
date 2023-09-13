# MST using KruskalΓÇÖs Algo


```md



```

# Approach - I
```cpp

/*
    Time Complexity: O(m * log(m) + n)
    Space Complexity: O(n + m)

    Where 'n' and 'm' denotes the number of nodes and edges in the graph, respectively.
*/

struct DSU
{
    vector<int> e;
    DSU(int n)
    {
        e = vector<int>(n, -1);
    }

    int parent(int x)
    {
        return e[x] < 0 ? x : e[x] = parent(e[x]);
    }

    int size(int x)
    {
        return -e[parent(x)];
    }

    bool union_sets(int x, int y)
    {  // union by size
        x = parent(x);
        y = parent(y);
        if (x == y) 
            return false;
        if (e[x] > e[y])
            swap(x, y);
        e[x] += e[y];
        e[y] = x;
        return true;
    }
};

// Custom comparator to sort the edges.
bool compare(vector <int> const &a, vector <int> const &b)
{
    return a[2] < b[2];
}

int kruskalMST(int n, vector<vector<int>> &edges)
{
    DSU d(n + 1);

    // To store the weight of MST.
    int cost = 0;

    // Sort the edges in ascending order by its weight.
    sort(edges.begin(), edges.end(), compare);

    // Start traversign through the edges.
    for (auto& edge: edges)
    {
        // Check if both vertices of current edge belong to different sets(subtrees).
        if (d.parent(edge[0]) != d.parent(edge[1]))
        {
            // Add the weight of the current edge.
            cost += edge[2];

            // Merge the two sets(subtrees).
            d.union_sets(edge[0], edge[1]);
        }
    }
    return cost;
}

```


