# Find the duplicate in an array of N+1 integers

### code

```cpp

#include <bits/stdc++.h>

// Find Duplicate Number

// This function finds the duplicate number in an array 'arr' of size 'n'.
// The function uses the Floyd's Tortoise and Hare algorithm to detect the duplicate.
// The duplicate number is returned as the result.

int findDuplicate(vector<int> &arr, int n) {
    int fast = 0, slow = 0;

    // Finding the intersection point of the two pointers
    do {
        fast = arr[arr[fast]]; // Fast pointer moves two steps at a time
        slow = arr[slow]; // Slow pointer moves one step at a time
    } while (fast != slow);

    // Resetting the slow pointer to the start
    slow = 0;

    // Moving both pointers at the same speed until they meet at the duplicate number
    while (fast != slow) {
        fast = arr[fast];
        slow = arr[slow];
    }

    return slow;
}


```