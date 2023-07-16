# Merge two Sorted Arrays Without Extra Space

### code

```cpp

#include <bits/stdc++.h>

// Merge Sorted Arrays

// This function merges two sorted arrays, arr1 and arr2, into a single sorted array.
// The merged array is stored in arr1, which is passed by reference.
// The function takes the sizes of arr1 (m) and arr2 (n) as input.
// The merged array is returned as the result.

vector<int> ninjaAndSortedArrays(vector<int>& arr1, vector<int>& arr2, int m, int n) {
    if (m == 0) {
        // If arr1 is empty, the merged array will be arr2.
        return arr2;
    }
    if (n == 0) {
        // If arr2 is empty, the merged array will be arr1.
        return arr1;
    }

    int l = m - 1; // Index of the last element in arr1
    int r = n - 1; // Index of the last element in arr2

    while (l >= 0 && r >= 0) {
        if (arr1[l] > arr2[r]) {
            // If the element in arr1 is greater, shift it to the right
            arr1[l + r + 1] = arr1[l];
            l--;
        } else {
            // If the element in arr2 is greater or equal, place it in the merged array
            arr1[l + r + 1] = arr2[r];
            r--;
        }
    }

    while (r >= 0) {
        // If there are remaining elements in arr2, copy them to the beginning of arr1
        arr1[r] = arr2[r];
        r--;
    }

    return arr1;
}


```