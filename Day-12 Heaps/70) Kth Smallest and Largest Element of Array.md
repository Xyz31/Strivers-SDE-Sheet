# Kth Smallest and Largest Element of Array


```md



```

Sample Input 1:
2
4 4
5 6 7 2
4 3
1 2 5 4


Sample Output 1:
7 2 
4 2


Explanation Of Sample Input 1:
Test case 1:
Here, ‘N’ = 4, ‘Arr’ = [5, 6, 7, 2] and ‘K’ = 3.
Elements of the array in ascending order are [2, 5, 6, 7]
Thus the 4rd smallest and 4rd largest elements of this array are 7 and 2 respectively.

Test case 2:
See problem statement for an explanation.

## code
```cpp


#include <queue>
#include <vector>

using namespace std;

 
// Partition the array around a pivot and return its index
// Complexity: O(n)
int partition(vector<int>& nums, int low, int high) {
    int pivot = nums[high];
    int i = low - 1;

    // Move elements smaller than or equal to the pivot to the left side
    // Complexity: O(n)
    for (int j = low; j <= high - 1; j++) {
        if (nums[j] <= pivot) {
            i++;
            swap(nums[i], nums[j]);
        }
    }

    // Move the pivot element to its correct position
    swap(nums[i + 1], nums[high]);
    return i + 1;
}

// Find the kth smallest element using Quickselect algorithm
// Complexity: O(n) on average, O(n^2) in the worst case
int quickselect(vector<int>& nums, int low, int high, int k) {
    if (low == high)
        return nums[low];

    // Partition the array and get the index of the pivot
    int pivotIndex = partition(nums, low, high);
    int leftLength = pivotIndex - low + 1;

    if (k == leftLength)
        return nums[pivotIndex];
    else if (k < leftLength)
        return quickselect(nums, low, pivotIndex - 1, k);
    else
        return quickselect(nums, pivotIndex + 1, high, k - leftLength);
}

// Find the kth smallest and kth largest elements in the array
// Complexity: O(n)
vector<int> kthSmallLarge(vector<int>& nums, int n, int k) {
    vector<int> ans;

    // Find the kth smallest element
    int kthSmallest = quickselect(nums, 0, n - 1, k);

    // Find the kth largest element
    int kthLargest = quickselect(nums, 0, n - 1, n - k + 1);

    ans.push_back(kthSmallest);
    ans.push_back(kthLargest);

    return ans;
}


```