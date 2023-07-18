# Longest substring without repeat

## code 

```cpp

#include <bits/stdc++.h> 

int uniqueSubstrings(string s)
{
    // Function to calculate the length of the longest substring with unique characters

    int n = s.size(); // Length of the input string
    vector<int> mpp(256, -1); // Map to store the last occurrence index of each character
    int left = 0; // Left pointer of the sliding window
    int right = 0; // Right pointer of the sliding window
    int len = 0; // Length of the longest substring with unique characters

    while (right < n) {
        if (mpp[s[right]] != -1) {
            // If the current character is already present in the substring, update the left pointer
            // to the next position after the last occurrence of the current character
            left = max(mpp[s[right]] + 1, left);
        }

        len = max(len, right - left + 1); // Update the length of the longest substring

        mpp[s[right]] = right; // Store the current index of the character in the map

        right++; // Move the right pointer to the next character
    }

    return len; // Return the length of the longest substring with unique characters
}


```