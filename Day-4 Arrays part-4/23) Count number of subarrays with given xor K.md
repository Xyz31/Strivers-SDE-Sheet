# count number of subarrays with given xor k

## code 

```cpp

#include <bits/stdc++.h>

int subarraysXor(vector<int>& arr, int x)
{
    // Variable to store the XOR of elements encountered so far
    int xr = 0;
    // Variable to keep track of the count of subarrays
    int count = 0;

    // Map to store the frequency of XOR values encountered
    std::map<int, int> mpp;

    // Initialize the map with the XOR value 0
    mpp[xr]++;

    // Iterate through the array elements
    for (auto it : arr) {
        // Update the XOR value by XORing with the current element
        xr = xr ^ it;
        // Calculate the required XOR value to obtain 'x'
        int k = xr ^ x;
        // Increment the count by the frequency of 'k' in the map
        count += mpp[k];
        // Increment the frequency of the current XOR value in the map
        mpp[xr]++;
    }

    // Return the total count of subarrays with XOR equal to 'x'
    return count;
}


```