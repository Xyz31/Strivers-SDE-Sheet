# Minimum Path Sum In a Grid


# Approach - I Brute Force
```cpp

/*
    Time Complexity: O(2 ^ (N + M))
    Space Complexity: O(N + M)

    Where 'N' is the number of rows and 'M' is the number of columns in grid.
*/

#include <limits.h>

int minSumHelper(vector<vector<int>> &grid, int i, int j, int n, int m) {
    // If indexes are out of range then return a very large value.
    if (i >= n || j >= m) {
        return INT_MAX;
    }

    // If it is bottom right end of the grid then return its value.
    if (i == n - 1 && j == m - 1) {
        return grid[i][j];
    }

    // Check in both the directions.
    int right = minSumHelper(grid, i, j + 1, n, m);
    int down = minSumHelper(grid, i + 1, j, n, m);

    // Calculate and return the current sum.
    int curSum = grid[i][j] + min(right, down);
    return curSum;
}

int minSumPath(vector<vector<int>> &grid) {
    int n = grid.size();
    int m = grid[0].size();

    // Calling the helper function to calculate the minimum sum path.
    int minSum = minSumHelper(grid, 0, 0, n, m);
    
    return minSum;
}



```

# Approach - II Recursive Memoization
```cpp

/*
    Time Complexity: O(N * M)
    Space Complexity: O(N * M)

    Where 'N' is the number of rows and 'M' is the number of columns in grid.
*/

#include <limits.h>

int minSumHelper(vector<vector<int>> &grid, vector<vector<int>> &lookUp, int i, int j, int n, int m) {   
    // If indexes are out of range then return a very large value.
    if (i >= n || j >= m) {
        return INT_MAX;
    }

    // If it is bottom right end of the grid then return its value.
    if (i == n - 1 && j == m - 1) {
        return grid[i][j];
    }

    // If the ans for subproblem already exist.
    if (lookUp[i][j] != -1) {
        return lookUp[i][j];
    }

    // Check in both the directions.
    int right = minSumHelper(grid, lookUp, i, j + 1, n, m);
    int down = minSumHelper(grid, lookUp, i + 1, j, n, m);

    // Storing the ans for furthur use.
    lookUp[i][j] = grid[i][j] + min(right, down);
    return lookUp[i][j];
}

int minSumPath(vector<vector<int>> &grid) {
    int n = grid.size();
    int m = grid[0].size();

    // Declaring a table to keep the value of already calculated subproblems.
    vector<vector<int>> lookUp(n, vector<int>(m, -1));

    // Calling the helper function to calculate the minimum sum path.
    int minSum = minSumHelper(grid, lookUp, 0, 0, n, m);
    return minSum;
}



```


# Approach - II Bottom Up DP
```cpp

/*
    Time Complexity: O(N * M)
    Space Complexity: O(1)

    Where 'N' is the number of rows and 'M' is the number of columns in grid.
*/

int minSumPath(vector<vector<int>> &grid) {
    int n = grid.size();
    int m = grid[0].size();

    // Iterating all the grid cells.
    for (int i = n - 1; i >= 0; i--) {
        for (int j = m - 1; j >= 0; j--) {   
            // If it is the bottom rightmost cell.
            if (i == n - 1 && j == m - 1) {
                continue;
            }
            // If the cell is in last row.
            else if (i == n - 1) {
                grid[i][j] = grid[i][j] + grid[i][j + 1];
            }
            // If the cell is in last column.
            else if (j == m - 1) {
                grid[i][j] = grid[i][j] + grid[i + 1][j];
            }
            // Else store the value which will be minimum of both the directions.
            else {
                grid[i][j] = grid[i][j] + min(grid[i + 1][j], grid[i][j + 1]);
            }
        }
    }
    // Return the minimum path sum.
    return grid[0][0];
}



```
