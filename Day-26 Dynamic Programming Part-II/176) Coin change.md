# Coin change


```md



```
 
# Approach - I Recursion
```cpp

/*
    Time Complexity: O(N * V)
    Space Complexity: O(N * V)
    
    where N is the length of denominations array and V is the value.
*/

#include <vector>

long countWaysToMakeChangeHelper(int denominations[], int value, int n, vector<vector<long>> &memo) 
{
    // if total is 0, return 1 (solution found)
    if (value == 0) 
    {
        return 1;
    }

    // return 0 (solution do not exist) if total become negative or
    // no elements are left
    if (n < 0 || value < 0) 
    {
        return 0;
    }

    if (memo[value][n] != -1)
    {
        return memo[value][n];
    }
    // Case 1. include current coin S[n] in solution and recur
    // with remaining change (N - S[n]) with same number of coins
    long incl = countWaysToMakeChangeHelper(denominations, value - denominations[n], n, memo);

    // Case 2. exclude current coin S[n] from solution and recur
    // for remaining coins (n - 1)
    long excl = countWaysToMakeChangeHelper(denominations, value, n - 1, memo);

    // return total ways by including or excluding current coin
    memo[value][n] = incl + excl;
    
    return memo[value][n];
}

long countWaysToMakeChange(int denominations[], int n, int value) 
{
    vector<vector<long>> memo(value + 1, vector<long>(n + 1, -1));
    return countWaysToMakeChangeHelper(denominations, value, n - 1, memo);
}

```

# Approach - II Recursion And Memoization
```cpp

/*
    Time Complexity: O(N * V)
    Space Complexity: O(N * V)
    
    where N is the length of denominations array and V is the value.
*/

#include <vector>

long countWaysToMakeChangeHelper(int denominations[], int value, int n, vector<vector<long>> &memo) 
{
    // if total is 0, return 1 (solution found)
    if (value == 0) 
    {
        return 1;
    }

    // return 0 (solution do not exist) if total become negative or
    // no elements are left
    if (n < 0 || value < 0) 
    {
        return 0;
    }

    if (memo[value][n] != -1)
    {
        return memo[value][n];
    }
    // Case 1. include current coin S[n] in solution and recur
    // with remaining change (N - S[n]) with same number of coins
    long incl = countWaysToMakeChangeHelper(denominations, value - denominations[n], n, memo);

    // Case 2. exclude current coin S[n] from solution and recur
    // for remaining coins (n - 1)
    long excl = countWaysToMakeChangeHelper(denominations, value, n - 1, memo);

    // return total ways by including or excluding current coin
    memo[value][n] = incl + excl;
    
    return memo[value][n];
}

long countWaysToMakeChange(int denominations[], int n, int value) 
{
    vector<vector<long>> memo(value + 1, vector<long>(n + 1, -1));
    return countWaysToMakeChangeHelper(denominations, value, n - 1, memo);
}

```


# Approach - II Iterative DP
```cpp

/*
    Time Complexity: O(N * V)
    Space Complexity: O(N * V)
    
    where N is the length of denominations array and V is the value.

*/

long countWaysToMakeChange(int *denominations, int n, int value)
{

    // Ways[i][j] will be storing the number of solutions of value j by last i coins.
    long **ways = new long *[n];

    for (int i = 0; i < n; i++)
    {
        ways[i] = new long[value + 1];
        ways[i][0] = 1;
    }

    for (int i = n - 1; i >= 0; i--)
    {
        for (int j = 1; j <= value; j++)
        {
            long count1 = 0;
            
            // By excluding the coin
            if (i + 1 <= n - 1)
            {
                count1 = ways[i + 1][j];
            }

            long count2 = 0;
            
            // By including the coin
            if (j - denominations[i] >= 0)
            {
                count2 = ways[i][j - denominations[i]];
            }

            ways[i][j] = count1 + count2;
        }
    }

    return ways[0][value];
}

```


# Approach - IV Space Optimised Iterative Approach
```cpp

/*
    Time Complexity: O(N * V)
    Space Complexity: O(V)
    
    where N is the length of denominations array and V is the value.

*/

long countWaysToMakeChange(int *denominations, int n, int value)
{
    // Dp[i] will be storing the number of solutions for value i.
    long *dp = new long[value + 1]();
    dp[0] = 1;

    for (int i = 0; i < n; i++)
    {
        for (int j = denominations[i]; j <= value; j++)
        {
            dp[j] += dp[j - denominations[i]];
        }
    }

    return dp[value];
}

```