# Rotate Matrix


### code 

```cpp

#include <bits/stdc++.h>

// Rotate Matrix

// Q7
// This function rotates a given matrix by 90 degrees clockwise.
void rotateMatrix(vector<vector<int>> &mat, int n, int m)
{
    int iu = 0, id = n - 1, jl = 0, jr = m - 1;

    while (jl < jr && iu < id) {
        int temp = mat[iu][iu];

        // Rotating the top row
        for (int j = jl + 1; j <= jr; j++) {
            swap(temp, mat[iu][j]);
        }

        // Rotating the rightmost column
        for (int i = iu + 1; i <= id; i++) {
            swap(temp, mat[i][jr]);
        }

        // Rotating the bottom row
        for (int j = jr - 1; j >= jl; j--) {
            swap(temp, mat[id][j]);
        }

        // Rotating the leftmost column
        for (int i = id - 1; i >= iu; i--) {
            swap(temp, mat[i][jl]);
        }

        iu++;
        id--;
        jl++;
        jr--;
    }

    return;
}


```