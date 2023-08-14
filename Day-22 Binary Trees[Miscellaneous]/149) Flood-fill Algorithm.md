# Flood-fill Algorithm

```md



```
 

# Approach - I Using Recursion
```cpp

/*
	Time complexity: O(M * N)
	Space Complexity: O(M * N)
	
	Where M and N are the number of rows and columns in the image, respectively.
*/

void floodFillHelper(vector<vector<int>> &image, int i, int j, int oldColor, int newColor)
{
    // Check if the current coordinates are valid or not.
    if (i < 0 || i >= image.size() || j < 0 || j >= image[0].size())
    {
        // Invalid coordinates. So, return.
        return;
    }

    if (image[i][j] != oldColor)
    {
        // Current pixel has a different colour than starting pixel.
        return;
    }

    if (image[i][j] == newColor)
    {
        // Current pixel has already been visited.
        return;
    }

    // Replace the colour of current pixel.
    image[i][j] = newColor;

    // Recur for adjacent pixels.
    floodFillHelper(image, i, j + 1, oldColor, newColor);
    floodFillHelper(image, i, j - 1, oldColor, newColor);
    floodFillHelper(image, i + 1, j, oldColor, newColor);
    floodFillHelper(image, i - 1, j, oldColor, newColor);
}

vector<vector<int>> floodFill(vector<vector<int>> &image, int x, int y, int newColor)
{
    int oldColor = image[x][y];

    floodFillHelper(image, x, y, oldColor, newColor);

    return image;
}

```

# Approach - II Using BFS

```cpp

/*
	Time complexity: O(M * N)
	Space Complexity: O(M * N)
	
	Where M and N are the number of rows and columns in the image, respectively.
*/

#include <queue>

vector<vector<int>> floodFill(vector<vector<int>> &image, int x, int y, int newColor)
{
    int oldColor = image[x][y];

    // Number of rows.
    int m = image.size();

    // Number of columns.
    int n = image[0].size();

    // Queue to hold the coordinates of the pixels.
    queue<pair<int, int>> q;

    q.push({x, y});

    while (!q.empty())
    {
        pair<int, int> currentPixel = q.front();
        q.pop();

        // i and j represent the row and column of the current pixel.
        int i = currentPixel.first;
        int j = currentPixel.second;


        // Check if the current coordinates are valid.
        if (i >= 0 && i < m && j >= 0 && j < n)
        {
            // Now, check if the current pixel has been colored or not.
            if (image[i][j] == oldColor && image[i][j] != newColor)
            {
                // So, replace the old colour.
                image[i][j] = newColor;

                // Push the adjacent pixels into the queue.
                q.push({i, j + 1});
                q.push({i, j - 1});
                q.push({i + 1, j});
                q.push({i - 1, j});
            }
        }
    }

    return image;
}

```