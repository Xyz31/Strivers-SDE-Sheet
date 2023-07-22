# Aggressive Cows


```cpp

#include <bits/stdc++.h> 

/*
int chessTournament(vector<int> positions , int n ,  int c){
	// Write your code here
}
*/


/*
 * This function calculates the minimum distance between chess players
 * in order to accommodate a given number of players in a given number
 * of rooms.
 *
 * @param positions: A vector containing the positions of chess players.
 * @param n: The number of chess players.
 * @param c: The number of rooms available.
 * @return: The minimum distance between chess players.
 */
int chessTournament(std::vector<int> positions, int n, int c) {
    // Sort the positions in ascending order
    sort(positions.begin(), positions.end());
    
    int ans = 0; // Variable to store the minimum distance
    int l = 1; // Left pointer for binary search
    int r = positions[n-1]; // Right pointer for binary search

    while (l <= r) {
        int mid = (l + r) >> 1; // Calculate the mid-point
        
        int count = 1; // Number of rooms used
        int previousRoom = positions[0]; // Position of the first player
        
        // Check if the current minimum distance allows accommodating 'c' players
        for (int i = 1; i < n; i++) {
            if (positions[i] - previousRoom >= mid) {
                count++;
                previousRoom = positions[i];
            }
        }

        if (count >= c) {
            ans = mid;
            l = mid + 1; // Move the left pointer to search for a larger distance
        } else {
            r = mid - 1; // Move the right pointer to search for a smaller distance
        }
    }

    return ans;
}

```