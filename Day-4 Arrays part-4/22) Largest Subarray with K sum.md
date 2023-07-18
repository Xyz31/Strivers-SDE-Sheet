# Largest Subarray with K sum

## code 

```cpp

#include <bits/stdc++.h>

// This function calculates the length of the longest subset with zero sum in the given array.
int LongestSubsetWithZeroSum(vector<int> arr) {

  // Create an unordered map to store the cumulative sum and its corresponding index.
  unordered_map<int, int> umap;
  int sum = 0;
  int len = 0;

  // Iterate over each element in the array.
  for (int i = 0; i < arr.size(); i++) {
    sum += arr[i];

    // Check if the current sum is zero.
    if (sum == 0) {
      // Update the length of the subset if the current sum is zero.
      len = max(len, i + 1);
    }

    // Check if the current sum has been encountered before.
    if (umap.find(sum) != umap.end()) {
      // Update the length of the subset if a subset with zero sum is found.
      len = max(len, i - umap[sum]);
    }

    // Check if the current sum has not been encountered before.
    if (umap.find(sum) == umap.end()) {
      // Store the current sum and its corresponding index in the unordered map.
      umap[sum] = i;
    }
  }

  // Return the length of the longest subset with zero sum.
  return len;

}


```