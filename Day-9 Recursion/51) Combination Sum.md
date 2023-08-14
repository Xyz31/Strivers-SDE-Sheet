# Combination Sum 
# Return Subsets Sum to K (Sum == K)

Sample Input 1:
3
2 4 6
6


Sample Output 1:
2 4
6


Explanation Of The Sample Input 1:

For the array'ARR' = {2, 4, 6}, we can have subsets {}, {2}, {4}, {6}, {2, 4}, {2, 6}, {4, 6}, {2, 4, 6}. Out of these 8 subsets, {2, 4} and {6} sum to the given 'K' i.e. 6. 

```md



```

## code
```cpp

// Recursive function to find subsets of an array that sum up to a given target value.
void solve(int ind, int n, int target, vector<int>& arr, vector<int>& temp, vector<vector<int>>& ans) {
    // Base case: Reached the end of the array
    if (ind == n) {
        // Check if the target sum is achieved
        if (target == 0) {
            // Add the current subset to the answer vector
            ans.push_back(temp);
        }
        return;
    }

    // Include the current element in the subset and recursively explore further
    temp.push_back(arr[ind]);
    solve(ind + 1, n, target - arr[ind], arr, temp, ans);

    // Exclude the current element from the subset and recursively explore further
    temp.pop_back();
    solve(ind + 1, n, target, arr, temp, ans);
}

// Function to find subsets of an array that sum up to a given target value.
vector<vector<int>> findSubsetsThatSumToK(vector<int> arr, int n, int k) {
    // Create a vector of vectors to store the subsets
    vector<vector<int>> ans;
    // Create a temporary vector to store the current subset being considered
    vector<int> temp;
    // Call the solve function to find the subsets
    solve(0, n, k, arr, temp, ans);
    // Return the resulting subsets
    return ans;
}


```