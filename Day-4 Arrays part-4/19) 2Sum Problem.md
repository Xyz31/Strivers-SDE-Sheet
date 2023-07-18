# 2Sum Problem

## code 

```cpp

#include <bits/stdc++.h>

// This function finds pairs in the given array whose sum is equal to s.
vector<vector<int>> pairSum(vector<int> &arr, int s){
   // Create an unordered map to store the frequency of elements in the array.
   unordered_map<int, int> umap;
   // Create a vector to store the pairs whose sum is equal to s.
   vector<vector<int>> ans;

   // Iterate over each element in the array.
   for(auto x : arr){
      // Check if there is a complement of x in the map.
      int count = umap[s - x];
      // Create a pair of numbers (x, complement) with the minimum number first.
      vector<int> pair(2);
      pair[0] = min(x, s - x);
      pair[1] = max(x, s - x);
      // Add the pair to the answer vector count number of times.
      while(count--){
         ans.push_back(pair);
      }
      // Increase the frequency of x in the map.
      umap[x]++;
   }

   // Sort the answer vector in ascending order.
   sort(ans.begin(), ans.end());
   // Return the answer vector.
   return ans;
}


```