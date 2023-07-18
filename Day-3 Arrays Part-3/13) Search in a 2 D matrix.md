# Search in a 2 D matrix

### code

```cpp

bool searchMatrix(vector<vector<int>>& mat, int target) {

    int m = mat.size(); // Number of rows in the matrix
    int n = mat[0].size(); // Number of columns in the matrix

    int lo = 0; // Lower bound index for binary search
    int hi = (n * m) - 1; // Upper bound index for binary search

    while (lo <= hi) {
        int mid = (lo + (hi - lo) / 2); // Calculate the middle index

        if (mat[mid / n][mid % n] == target) // Check if the middle element is equal to the target
            return true;
        
        if (mat[mid / n][mid % n] < target) // If the middle element is smaller than the target, search in the right half
            lo = mid + 1;
        else // If the middle element is greater than the target, search in the left half
            hi = mid - 1;
    }

    return false; // Target not found in the matrix
}


```