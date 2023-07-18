# Majority Element (>n/2 times) - 

### code


```cpp

#include <bits/stdc++.h>


int findMajorityElement(int arr[], int n) {
	// Find the majority element in the array, if exists

	int count = 0; // Variable to keep track of count
	int element; // Variable to store the potential majority element

	// Iterate through the array
	for (int i = 0; i < n; i++) {
		int x = arr[i]; // Current element

		if (count == 0) {
			// If count is 0, set the current element as the potential majority element
			element = x;
			count++;
		} else if (element == x) {
			// If the current element is the same as the potential majority element, increment count
			count++;
		} else {
			// If the current element is different from the potential majority element, decrement count
			count--;
		}
	}

	int cnt = 0; // Variable to count the occurrences of the potential majority element

	// Count the occurrences of the potential majority element in the array
	for (int i = 0; i < n; i++) {
		if (element == arr[i]) {
			cnt++;
		}
	}

	// Check if the potential majority element occurs more than (n/2) times
	if (cnt >= (n / 2) + 1) {
		return element; // Return the majority element
	}

	return -1; // Return -1 if no majority element exists
}


```