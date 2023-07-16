# Problem Statement

Given an 'N' x "M' integer matrix, if an element is 0, set its entire row and
column to 0's, and return the matrix. In particular, your task is to modify it in
such a way that if a cell has a value 0 (matrix [i] i] == 0), then all the cells of
the ith row and jth column should be changed to 0.
You must do it in place.

For Example:

If the given grid is this: 
[7, 19, 3]
[4, 21, 0]
Then the modified grid will be:
[7, 19, 0]
[0, 0, 0]


###Code

```cpp

#include <bits/stdc++.h>

void setZeros(vector<vector<int>> &matrix)
{
	// Write your code here.
	//Striver's solution

	if (matrix.empty()) {
        return;
    }

    int m = matrix.size();
    int n = matrix[0].size();
    bool firstRowZero = false;
    bool firstColZero = false;

    // Check if the first row should be zeroed
    for (int j = 0; j < n; j++) {
        if (matrix[0][j] == 0) {
            firstRowZero = true;
            break;
        }
    }

    // Check if the first column should be zeroed
    for (int i = 0; i < m; i++) {
        if (matrix[i][0] == 0) {
            firstColZero = true;
            break;
        }
    }

    // Use the first row and first column as markers
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            if (matrix[i][j] == 0) {
                matrix[i][0] = 0;
                matrix[0][j] = 0;
            }
        }
    }

    // Set the zeros based on the markers
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                matrix[i][j] = 0;
            }
        }
    }

    // Zero out the first row if necessary
    if (firstRowZero) {
        for (int j = 0; j < n; j++) {
            matrix[0][j] = 0;
        }
    }

    // Zero out the first column if necessary
    if (firstColZero) {
        for (int i = 0; i < m; i++) {
            matrix[i][0] = 0;
        }
    }

}

```