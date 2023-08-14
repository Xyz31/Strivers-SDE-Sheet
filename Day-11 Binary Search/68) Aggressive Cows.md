# Aggressive Cows


Sample Input 2 :
2
4 2
5 4 2 1
6 4
6 7 9 13 15 11


Sample Output 2 :
4
2


Explanation For Sample Output 2:
In test case 1, 
we only have to allocate rooms to 2 players so we can assign rooms that are first and last which are 1 and 5, so our answer is 5 - 1 = 4.

In test case 2, 
there is no way by which we can allocate rooms such that every player will have the 3 or more as its least distance to other players. So the answer is 2 and one possible allocation of rooms is as follows.
    Player1 = 6
    Player2 = 9
    Player3 = 11
    Player4 = 13 


```md



```

## code
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
int chessTournament(vector<int> positions, int n, int c) {
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