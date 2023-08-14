# Find Minimum Number Of Coins

Sample Input 1
13


Sample Output 1
10 2 1


Explanation Of Sample Input 1
The minimum number of coins to change is 3 {1, 2, 10}.

```md



```

## code
```cpp

#include <bits/stdc++.h> 

// Function to find the minimum number of coins required to make the given amount
int findMinimumCoins(int amount) {
    int ans = 0; // Variable to store the minimum number of coins
    int coins[] = {1, 2, 5, 10, 20, 50, 100, 500, 1000}; // Array of available coin denominations

    // Iterate through the coin denominations in reverse order
    for (int i = 9 - 1; i >= 0; i--) {
        // Check if the current coin denomination can be used to make change for the remaining amount
        if (amount >= coins[i]) {
            int k = amount / coins[i]; 
            // Number of coins needed for the current denomination
            ans += k; 
            // Increment the answer by the number of coins needed
            amount -= k * coins[i]; 
            // Reduce the remaining amount by the value of the coins used
        }
    }

    return ans; // Return the minimum number of coins
}

```