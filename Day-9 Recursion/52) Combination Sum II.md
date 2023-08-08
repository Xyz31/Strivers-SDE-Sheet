# Combination Sum II

Modification of combination sum 1 to handle the cases of duplicate elements

```cpp

#include<algorithm>


void solve(int ind, int n, int target, vector<int>& arr, vector<int>& temp, vector<vector<int>>& ans) {
    if (target == 0) {
        // Target sum achieved, add the current subset to the answer vector
        ans.push_back(temp);
        return;
    }

    for (int i = ind; i < n; i++) {
        // Skip duplicates at the same level
        if (i > ind && arr[i] == arr[i - 1])
            continue;

        if (arr[i] <= target) {
            // Include the current element in the subset and recursively explore further
            temp.push_back(arr[i]);
            solve(i + 1, n, target - arr[i], arr, temp, ans);
            temp.pop_back(); // Backtrack: Remove the last element from the subset
        }
    }
}

vector<vector<int>> combinationSum2(vector<int> &arr, int n, int target){
    vector<vector<int>> ans;
    vector<int> temp;
    sort(arr.begin(),arr.end()); // Sort the input array in non-decreasing order
    solve(0, n, target, arr, temp, ans); // Call the solve function to find subsets
    return ans; // Return the resulting subsets
}




```