# Largest rectangle in a histogram

```md



```

# Approach-I
```cpp

/*
    Time Complexity = O(N^2)
    Space Complexity = O(1)
    
    Where N is the number of elements in the given array/list.
*/

int largestRectangle(vector < int > & heights) {
    int n = heights.size();

    if (n <= 0) {
        return 0;
    }

    int maxArea = 0;

    for (int j = 0; j < n; j++) {
        // Store current index value as both min and max values.
        int minVal = heights[j], maxVal = heights[j];

        for (int i = j - 1; i >= 0; i--) {
            // If current index value is less than minVal.
            if (heights[i] < minVal) {
                minVal = heights[i];
            }

            /*
            	If area of the current rectangle 
                is greater than maxVal.
            */
            if (minVal * (j - i + 1) > maxVal) {
                maxVal = minVal * (j - i + 1);
            }
        }

        // Store the maximum area of the rectangle.
        if (maxVal > maxArea) {
            maxArea = maxVal;
        }
    }

    // Return area of largest rectangle.
    return maxArea;
}

```

# Approach-II
```cpp

/*
    Time Complexity = O(N*log(N))
    Space Complexity = O(N)
    
    Where N is the number of elements in the given array/list.
*/

// Segment Tree Class
class SegTreeNode 
{
    public:
    int start;
    int end;
    int min;
    SegTreeNode * left;
    SegTreeNode * right;

    SegTreeNode(int start, int end) 
    {
        this -> start = start;
        this -> end = end;
        left = right = NULL;
    }
};

int query(SegTreeNode *root, vector<int> &heights, int start, int end) 
{ 
    // The range of current root is out of range
    if (root == NULL || end < root -> start || start > root -> end) 
      return -1;
    
    // The range of current root is in the range
    if (start <= root -> start && end >= root -> end) 
    {
        return root -> min;
    }
    
    int leftMin = query(root -> left, heights, start, end);
    int rightMin = query(root -> right, heights, start, end);
    
    if (leftMin == -1) 
      return rightMin;
    
    if (rightMin == -1) 
      return leftMin;
    
    return heights[leftMin] < heights[rightMin] ? leftMin : rightMin;
}

int calculateMax(vector<int> &heights, SegTreeNode *root, int start, int end) 
{
  // Check if start is greater than end
    if (start > end) 
    {
        return -1;
    }
    
    // If there is only one element in the histogram
    if (start == end) 
    {
        return heights[start];
    }
    
    int minIndex = query(root, heights, start, end);
    int leftMax = calculateMax(heights, root, start, minIndex - 1);
    int rightMax = calculateMax(heights, root, minIndex + 1, end);
    int minMax = heights[minIndex] * (end - start + 1);
    
    return max(max(leftMax, rightMax), minMax);
}

SegTreeNode* buildSegmentTree(vector<int> &heights, int start, int end) 
{
    if (start > end)
    { 
      return NULL;
    }
    
    // Creating a node for the current range
    SegTreeNode *root = new SegTreeNode(start, end);
    
    if (start == end) 
    {
        root -> min = start;
        return root;
    } 
    else 
    {
        int middle = (start + end) / 2;
        
        // Creating recursive calls for left and right subtree
        root -> left = buildSegmentTree(heights, start, middle);
        root -> right = buildSegmentTree(heights, middle + 1, end);
        root -> min = heights[root -> left -> min] < heights[root -> right -> min] ? root -> left -> min : root -> right -> min;
        
        return root;
    }
}

int largestRectangle(vector<int> &heights) 
{
    if (heights.size() == 0)
        return 0;

    // Build a segment tree
    SegTreeNode *root = buildSegmentTree(heights, 0, heights.size() - 1);

    // Calculate the maximum area recursively
    return calculateMax(heights, root, 0, heights.size() - 1);
}

```

# Approach-III
```cpp


#include <stack>
#include <vector>

/*
    Time Complexity = O(N)
    Space Complexity = O(N)
    
    Where N is the number of elements in the given array/list.
*/

// Function to calculate the largest rectangle area in a histogram
int largestRectangle(std::vector<int>& heights) {
    int n = heights.size(); // Get the number of elements in the input vector
    if (n == 0) return 0; // If the vector is empty, the maximum area is 0
    
    std::stack<int> st; // Stack to store the indices of the histogram bars
    
    int maxArea = 0; // Variable to store the maximum area
    
    for (int i = 0; i <= n; i++) {
        int height = (i == n) ? 0 : heights[i]; // Set the current bar's height or 0 if it's beyond the vector
        
        // Process bars in non-decreasing order of heights
        while (!st.empty() && height <= heights[st.top()]) {
            int poppedHeight = heights[st.top()]; // Get the height of the bar at the top of the stack
            st.pop(); // Pop the index of the bar
            
            int width = st.empty() ? i : i - st.top() - 1; // Calculate the width of the rectangle
            
            maxArea = std::max(maxArea, poppedHeight * width); // Update the maximum area if necessary
        }
        
        st.push(i); // Push the current index to the stack
    }
    
    return maxArea; // Return the maximum area of the largest rectangle
}



```
