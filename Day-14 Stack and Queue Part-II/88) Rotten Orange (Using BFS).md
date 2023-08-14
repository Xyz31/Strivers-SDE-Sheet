# Rotten Orange (Using BFS)

```md



```

# Approach - I
```cpp

/*
    Time Complexity - O(N * M * max(N, M))
    Space Complexity - O(1)

    where N and M are the number of rows and columns of
    the grid respectively.
*/


int isValid(int i, int j, int n, int m)
{
    return i >= 0 && i < n && j >= 0 && j < m;
}

int rottenOranges(vector<vector<int>>& grid)
{

    int n = grid.size();
    int m = grid[0].size();

    int currRotten = 2, time = 0;

    // Array for exploring all 4 directions.
    int dx[] = {0, 0, 1, -1};
    int dy[] = {1, -1, 0, 0};

    while (true)
    {
        bool notFound = true;;

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {
                if (grid[i][j] == currRotten)
                {
                    notFound = false;

                    // Check all adjacent cells and rot them, if valid.
                    // Assign them different value (currRottenNum + 1).
                    for (int k = 0; k < 4; k++)
                    {
                        int nextI = i + dx[k];
                        int nextJ = j + dy[k];

                        if (isValid(nextI, nextJ, n, m) && grid[nextI][nextJ] == 1)
                        {
                            grid[nextI][nextJ] = currRotten + 1;
                        }
                    }
                }
            }
        }

        // If no rotten oranges is present to process, break.
        if (notFound)
        {
            break;
        }
        currRotten++;
        time++;
    }

    // Iterate to check is any fresh orange left.
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            if (grid[i][j] == 1)
            {
                return -1;
            }
        }
    }

    // Return time taken.
    return max(0, time - 1);
}

```

# Approach - II
```cpp

/*
    Time Complexity - O(N * M)
    Space Complexity - O(N * M)

    where N and M are the number of rows and columns of the grid respectively.

    Function to find the minimum number of days required to rot all oranges in the grid.
    If all oranges cannot be rotted, it returns -1.
    The function uses BFS (Breadth-First Search) algorithm to traverse the grid.

    Parameters:
    - grid: a reference to a 2D vector representing the grid with integer values:
            0 - empty cell
            1 - fresh orange
            2 - rotten orange

    Returns:
    - The minimum number of days required to rot all oranges or -1 if it is not possible to rot all oranges.

    Note: The function assumes that the grid is valid and contains either 0, 1, or 2 as its elements.
*/

int rottenOranges(vector<vector<int>>& grid) {
    if(grid.empty()) return 0; // If the grid is empty, there are no oranges to rot, so return 0.

    int m = grid.size(); // Number of rows in the grid.
    int n = grid[0].size(); // Number of columns in the grid.
    int days = 0; // Variable to keep track of the number of days taken to rot all oranges.
    int tot = 0; // Variable to count the total number of oranges in the grid.
    int cnt = 0; // Variable to count the number of rotten oranges.

    queue<pair<int, int>> rotten; // Queue to store the coordinates of rotten oranges.

    // Loop through the entire grid to count the total oranges and push rotten oranges into the queue.
    for(int i = 0; i < m; ++i){
        for(int j = 0; j < n; ++j){
            if(grid[i][j] != 0) // If the cell is not empty, increment the total orange count.
                tot++;
            if(grid[i][j] == 2) // If the cell contains a rotten orange, push its coordinates into the queue.
                rotten.push({i, j});
        }
    }

    int dx[4] = {0, 0, 1, -1}; // Arrays for exploring all 4 directions (up, down, left, right).
    int dy[4] = {1, -1, 0, 0};

    // Perform BFS until the queue of rotten oranges is empty.
    while(!rotten.empty()){
        int k = rotten.size(); // Number of oranges at the current level (current day).
        cnt += k; // Increment the count of rotten oranges with the number of oranges at the current level.

        while(k--){
            int x = rotten.front().first, y = rotten.front().second; // Get the coordinates of the current rotten orange.
            rotten.pop(); // Remove the current rotten orange from the queue.

            // Check all adjacent cells and if they contain fresh oranges, make them rotten and add to the queue.
            for(int i = 0; i < 4; ++i){
                int nx = x + dx[i], ny = y + dy[i]; // Calculate the coordinates of the adjacent cell.

                // If the adjacent cell is outside the grid boundaries or contains a non-fresh orange, skip it.
                if(nx < 0 || ny < 0 || nx >= m || ny >= n || grid[nx][ny] != 1)
                    continue;

                grid[nx][ny] = 2; // Mark the adjacent fresh orange as rotten.
                rotten.push({nx, ny}); // Add the rotten orange's coordinates to the queue for the next level (next day).
            }
        }

        if(!rotten.empty()) // If the queue is not empty, there are more oranges to rot, so increment the days count.
            days++;
    }

    // If the total number of oranges in the grid is equal to the count of rotten oranges,
    // it means all oranges have been rotted, so return the number of days taken.
    // Otherwise, return -1, indicating that not all oranges could be rotted.
    return tot == cnt ? days : -1;
}


```