# Longest Consecutive Sequence

## code 

```cpp

#include <bits/stdc++.h>

// This function calculates the length of the longest consecutive sequence in the array.
int lengthOfLongestConsecutiveSequence(vector<int> &arr, int n) {
    // Create an unordered set to store the elements of the array.
    unordered_set<int> hashset;

    // Insert all elements of the array into the hashset.
    for(auto x : arr){
        hashset.insert(x);
    }

    // Initialize the variable to store the length of the longest consecutive sequence.
    int longeststreak = 1;

    // Iterate over each element in the array.
    for(auto num : arr){
        // Check if the previous consecutive element (num-1) is not present in the hashset.
        if(!hashset.count(num - 1)){
            int next = num;
            int streak = 1;

            // Continue incrementing next and counting the streak as long as the consecutive elements are present in the hashset.
            while(hashset.count(next + 1)){
                next++;
                streak++;
            }

            // Update the longest streak if the current streak is longer.
            longeststreak = max(longeststreak, streak);
        }
    }

    // Return the length of the longest consecutive sequence.
    return longeststreak;
}


```