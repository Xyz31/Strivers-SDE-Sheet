# 4Sum Problem

## code 

```cpp

#include <bits/stdc++.h>

// This function checks if there exists a quadruplet in the array whose sum is equal to the target.
string fourSum(vector<int> arr, int target, int n) {
    // Create an unordered map to store the sum of all pairs of elements in the array.
    unordered_map<int, pair<int, int>> mp;

    // Calculate the sum of all pairs of elements in the array and store them in the map.
    for(int i = 0; i < n - 1; i++)
    {
        for(int j = i + 1; j < n; j++)
        {
            int sum = arr[i] + arr[j];
            // Store the pair of indices (i, j) corresponding to the sum in the map.
            mp[sum] = {i, j};
        }
    }

    // Iterate over each pair of elements in the array.
    for(int i = 0; i < n - 1; i++)
    {
        for(int j = i + 1; j < n; j++)
        {
            // Calculate the required sum to form a quadruplet.
            int left = target - (arr[i] + arr[j]);

            // Check if the complement of the sum exists in the map.
            if(mp.find(left) != mp.end())
            {
                // Retrieve the pair of indices corresponding to the complement sum.
                pair<int, int> it = mp[left];
                int k = it.first;
                int l = it.second;

                // Check if the indices are all distinct, indicating a valid quadruplet.
                if(i != k && i != l && j != k && j != l)
                    return "Yes";
            }
        }
    }

    // No valid quadruplet was found.
    return "No";
}


```