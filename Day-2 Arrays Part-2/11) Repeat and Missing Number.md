# 	Repeat and Missing Number

### code

```cpp

#include <bits/stdc++.h>

pair<int, int> missingAndRepeating(vector<int> &arr, int n) {
  // Write your code here

  int missing_no = 0, repeating_no = 0;

  // Calculate XOR of all elements in the array
  int xor1 = arr[0];
  for (int i = 1; i < n; i++) {
    xor1 ^= arr[i];
  }

  // Calculate XOR of all numbers from 1 to n
  for (int i = 1; i <= n; i++) {
    xor1 ^= i;
  }

  // Find the rightmost set bit in XOR
  int set_bit_no = xor1 & -xor1;

  // Divide the elements into two groups based on the set bit
  for (int i = 0; i < n; i++) {
    if (set_bit_no & arr[i])
      missing_no ^= arr[i];
    else
      repeating_no ^= arr[i];
  }

  // Divide the numbers from 1 to n into two groups based on the set bit
  for (int i = 1; i <= n; i++) {
    if (set_bit_no & i)
      missing_no ^= i;
    else
      repeating_no ^= i;
  }

  // Check if missing_no or repeating_no is equal to any element in the array
  for (int i = 0; i < n; i++) {
    if (arr[i] == missing_no)
      return {repeating_no, missing_no};
    else if (arr[i] == repeating_no)
      return {missing_no, repeating_no};
  }
}


```