# M Coloring Problem


Sample Input 1:
3 2
0 1 0
1 0 1
0 1 0


Sample Output 1:
YES


Explanation Of Input 1:
The adjacency matrix tells us that 1 is connected to 2, and 2 is connected to 3. We can see that a minimum of 2 colors would be needed to color the graph. So it is possible to color the graph in this case.

```md



```

## code
```cpp

// Function to check if it is safe to assign a particular color to a node
bool isSafe(int col, int node, int n, vector<int>& color, vector<vector<int>>& mat) {
    for (int k = 0; k < n; k++) {
        // Check all neighboring nodes (except the current node) for color conflicts
        if (k != node && mat[k][node] == 1 && color[k] == col) {
            return false; // Color conflict found, not safe to assign the color
        }
    }
    return true; // No color conflicts found, safe to assign the color
}

// Backtracking function to solve the graph coloring problem
bool solve(int node, int n, int m, vector<int>& color, vector<vector<int>>& mat) {
    if (node == n) {
        return true; // All nodes have been colored, solution found
    }

    for (int i = 1; i <= m; i++) {
        if (isSafe(i, node, n, color, mat) == true) {
            color[node] = i; // Assign the color to the current node

            // Recursively solve for the next node
            if (solve(node + 1, n, m, color, mat)) {
                return true; // Solution found
            }

            color[node] = 0; // Backtrack: reset the color of the current node
        }
    }

    return false; // No solution found
}

// Main function to check if graph coloring is possible with 'm' colors
string graphColoring(vector<vector<int>>& mat, int m) {
    int n = mat.size(); // Number of nodes in the graph
    vector<int> color(n, 0); // Initialize the color vector with all nodes uncolored

    // Call the solve function to find a valid coloring
    if (solve(0, n, m, color, mat) == true) {
        return "YES"; // Graph coloring is possible with 'm' colors
    }

    return "NO"; // Graph coloring is not possible with 'm' colors
}


```