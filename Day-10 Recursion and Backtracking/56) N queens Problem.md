# N queens Problem

```cpp

/*
    Time Complexity : O(N!)
    Space Complexity : O(N)
    
    Where N is the number of Queens.
*/

void addSolution(int n, vector < vector < int >> & ans, vector < int > & row) {
    vector < int > currentAnswer;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (row[j] == i) {
                currentAnswer.push_back(1);
            } else {
                currentAnswer.push_back(0);
            }
        }
    }

    ans.push_back(currentAnswer);
}

void solve(int col, int n, vector < vector < int >> & ans, vector < int > & row, vector < int > & d1, vector < int > & d2) {
    if (col == n) {
        addSolution(n, ans, row);
        return;
    }

    for (int i = 0; i < n; i++) {
        if ((row[i] == -1) && (d1[col - i + n - 1] == -1) && (d2[col + i] == -1)) {
            row[i] = d1[col - i + n - 1] = d2[col + i] = col;
            solve(col + 1, n, ans, row, d1, d2);
            row[i] = d1[col - i + n - 1] = d2[col + i] = -1;
        }
    }

    return;
}

vector < vector < int >> solveNQueens(int n) {
    vector < vector < int >> ans;
    vector < int > row(30, -1), d1(30, -1), d2(30, -1);
    solve(0, n, ans, row, d1, d2);
    return ans;
}

/*

// This function checks if placing a queen at a given column and row is safe or not.
bool isSafe(int col, int row, int n, vector<vector<int>> temp) {
    int c = col;
    int r = row;

    // Checking the upper-left diagonal for any queen
    while (r >= 0 && c >= 0) {
        if (temp[r][c] == 1) {
            return false;
        }
        r--, c--;
    }

    c = col;
    r = row;

    // Checking the left column for any queen
    while (c >= 0) {
        if (temp[r][c] == 1) {
            return false;
        }
        c--;
    }

    c = col;
    r = row;

    // Checking the lower-left diagonal for any queen
    while (r < n && c >= 0) {
        if (temp[r][c] == 1) {
            return false;
        }
        r++, c--;
    }

    // It is safe to place a queen at the given column and row
    return true;
}

// This function solves the N-Queens problem using backtracking.
void solve(int col, int k, int n, vector<vector<int>>& temp, vector<vector<int>>& ans) {
    // Base case: All columns have been filled, i.e., we have found a valid solution.
    if (col == n) {
        // Store the current arrangement of queens in the answer vector
        vector<int> store;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                store.push_back(temp[i][j]);
            }
        }
        ans.push_back(store);
        return;
    }

    // Recursive case: Try placing a queen in each row of the current column
    for (int row = 0; row < n; row++) {
        if (isSafe(col, row, n, temp)) {
            temp[row][col] = 1; // Place a queen at the current position
            solve(col + 1, k, n, temp, ans); // Recur for the next column
            temp[row][col] = 0; // Backtrack and remove the queen from the current position
        }
    }
}

vector<vector<int>> solveNQueens(int n) {
    vector<vector<int>> temp(n, vector<int>(n, 0)); // Create an empty chessboard
    vector<vector<int>> ans; // Store all valid solutions

    // Start solving the N-Queens problem from the first column (col = 0)
    solve(0, 0, n, temp, ans);

    return ans; // Return the list of valid solutions
}

*/

```