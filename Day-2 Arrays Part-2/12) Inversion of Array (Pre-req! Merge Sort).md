# Inversion of Array (Pre-req: Merge Sort)


### code 

```cpp

#include <bits/stdc++.h>

// Merge the two sorted arrays and count inversions while merging
long long merge(long long *arr, long long *temp, int left, int mid, int right) {
   int i, j, k;
   long long count = 0;
   i = left; // i to locate the first array's location
   j = mid; // j to locate the second array's location
   k = left; // k to locate the merged array's location

   while ((i <= mid - 1) && (j <= right)) {
      if (arr[i] <= arr[j]) { // When the left item is less than the right item
         temp[k++] = arr[i++];
      } else {
         temp[k++] = arr[j++];
         count += (mid - i); // Find how many inversions are performed
      }
   }

   while (i <= mid - 1) // If the first list has remaining items, add them to the list
      temp[k++] = arr[i++];

   while (j <= right) // If the second list has remaining items, add them to the list
      temp[k++] = arr[j++];

   for (i = left; i <= right; i++)
      arr[i] = temp[i]; // Store the temporary array into the main array

   return count;
}

long long mergeSort(long long *arr, long long *temp, int left, int right) {
   long long mid, count = 0;

   if (right > left) {
      mid = (right + left) / 2; // Find the mid-index of the array
      count = mergeSort(arr, temp, left, mid); // Merge sort the left subarray
      count += mergeSort(arr, temp, mid + 1, right); // Merge sort the right subarray
      count += merge(arr, temp, left, mid + 1, right); // Merge two subarrays
   }

   return count;
}

long long getInversions(long long *arr, int n) {
    // Write your code here.
    std::vector<long long> temp(n);
    long long ans = mergeSort(arr, temp.data(), 0, n - 1);
    return ans;
}


```