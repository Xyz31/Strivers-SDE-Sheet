# Rat in a Maze


Sample Input 1 :
3
1 0 1
1 0 1
1 1 1


Sample Output 1 :
1 0 0 1 0 0 1 1 1 


Explanation For Sample Output 1:
Only 1 path is possible which contains coordinate < (1,1), (2,1), (3,1), (3,2) and (3,3) >

So our path matrix will look like this:

1 0 0
1 0 0
1 1 1

Which is returned from left to right and then top to bottom in one line.


```md



```

## code
```cpp



#include <bits/stdc++.h>

// Function to solve the maze using backtracking
void solve(int row, int col, int n, vector<vector<int>>& maze, vector<vector<int>>& visit, vector<vector<int>>& ans) {
    // Check if the current position is out of bounds or already visited or is a wall (0)
    if (row < 0 || col < 0 || row >= n || col >= n || visit[row][col] || maze[row][col] == 0) {
        return;
    }

    // Mark the current position as visited
    visit[row][col] = 1;

    // Check if we reached the destination (bottom-right cell of the maze)
    if (row == n - 1 && col == n - 1) {
        // If destination reached, add the current path to the answer
        vector<int> temp;
        for (auto x : visit) {
            for (auto y : x) {
                temp.push_back(y);
            }
        }
        ans.push_back(temp);
    }

    // Explore all possible directions: Up, Down, Left, Right
    solve(row - 1, col, n, maze, visit, ans); // Up
    solve(row + 1, col, n, maze, visit, ans); // Down
    solve(row, col - 1, n, maze, visit, ans); // Left
    solve(row, col + 1, n, maze, visit, ans); // Right

    // Mark the current position as unvisited (backtracking)
    visit[row][col] = 0;
}

// Main function to find all paths in the maze
vector<vector<int>> ratInAMaze(vector<vector<int>>& maze, int n) {
    // Create a matrix to track visited cells
    vector<vector<int>> visit(n, vector<int>(n, 0));
    // Initialize the answer vector
    vector<vector<int>> ans;

    // Check if the starting cell is a valid path (1)
    if (maze[0][0] == 1) {
        solve(0, 0, n, maze, visit, ans); // Start solving the maze from the top-left cell
    }

    return ans; // Return the list of all possible paths
}

```