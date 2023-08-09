# Merge K Sorted Arrays


```md
Sample Input 1:
1
2
3 
3 5 9 
4 
1 2 3 8 


Sample Output 1:
1 2 3 3 5 8 9 


Explanation Of Sample Input 1:
After merging the two given arrays/lists [3, 5, 9] and [ 1, 2, 3, 8], the output sorted array will be [1, 2, 3, 3, 5, 8, 9].


```
## code
```cpp

#include <bits/stdc++.h>

// Function to merge two sorted arrays 'a' and 'b' into a single sorted array 'res'
vector<int> mergeTwoSortedArr(vector<int>& a, vector<int>& b) {
    vector<int> res;
    int n = a.size();
    int m = b.size();
    int i = 0, j = 0;

    // Merge 'a' and 'b' in sorted order into 'res'
    while (i < n && j < m) {
        if (a[i] < b[j]) {
            res.push_back(a[i]);
            i++;
        } else {
            res.push_back(b[j]);
            j++;
        }
    }

    // Add any remaining elements from 'a' and 'b' to 'res'
    while (i < n) {
        res.push_back(a[i]);
        i++;
    }
    while (j < m) {
        res.push_back(b[j]);
        j++;
    }
    return res; // Return the merged sorted array
}

// Function to merge 'k' sorted arrays represented by 'kArr' from index 'i' to index 'j'
vector<int> mergeKArrays(vector<vector<int>>& kArr, int i, int j) {
    if (i == j) {
        return kArr[i]; // Base case: When only one array remains, return it as the merged array
    }

    int mid = (i + j) / 2; // Calculate the middle index
    vector<int> left = mergeKArrays(kArr, i, mid); // Recursively merge the left half of arrays
    vector<int> right = mergeKArrays(kArr, mid + 1, j); // Recursively merge the right half of arrays

    // Merge the left and right halves into a single sorted array and return it
    return mergeTwoSortedArr(left, right);
}

// Function to merge 'k' sorted arrays represented by 'kArrays'
vector<int> mergeKSortedArrays(vector<vector<int>>& kArrays, int k) {
    // Call the helper function 'mergeKArrays' to merge all 'k' arrays from index 0 to index k-1
    return mergeKArrays(kArrays, 0, k - 1);
}


```