# Matrix Median


```cpp


/*
int getMedian(vector<vector<int>> &matrix)
{
    // Write your code here.
}
*/

#include <vector>
#include <algorithm>

int getMedian(std::vector<std::vector<int>>& matrix)
{
    std::vector<int> flattened;
    const int rows = matrix.size();
    const int cols = matrix[0].size();

    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            flattened.push_back(matrix[i][j]);
        }
    }

    std::sort(flattened.begin(), flattened.end());

    const int totalElements = flattened.size();
    const int middleIndex = totalElements / 2;

    if (totalElements % 2 == 0) {
        // Even number of elements
        return (flattened[middleIndex - 1] + flattened[middleIndex]) / 2;
    } else {
        // Odd number of elements
        return flattened[middleIndex];
    }
}


```