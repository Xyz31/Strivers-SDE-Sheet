# Matrix Median

Sample Input 1:
2
1 3
1 2 3
3 3
2 6 9
1 5 11
3 7 8


Sample Output 1:
2
6


Explanation Of Sample Input 1:
In the first test case, the overall median of the matrix is 2.

In the second test case, the overall median of the matrix is 6.

## code
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