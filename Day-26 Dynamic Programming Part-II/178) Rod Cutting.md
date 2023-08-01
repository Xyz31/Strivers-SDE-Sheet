# Rod Cutting



# Approach - I Recursive Approach
```cpp

/*
    Time complexity = O(2 ^ N)
    Space complexity = O(N)

    Where 'N' is the length of the rod.
*/

int cutRod(vector<int> &price, int n)
{
    // Base condition.
    if (n <= 0)
    {
        return 0;
    }

    // Inialize maxCost with minimum value.
    int maxCost = INT_MIN;

    /*
       Recursively cut the rod, obtain different configurations
       And compare cost obtained from each with maxCost.
    */
    for (int i = 0; i < n; i++) {
        maxCost = max(maxCost, price[i] + cutRod(price, n - i - 1));
    }

    return maxCost;
}


```


# Approach - II Top-down dp approach
```cpp

/*
    Time Complexity : O(N ^ 2)
    Space Complexity : O(N ^ 2)

    Where 'N' is the length of the rod.
*/

#include <cstring>
using namespace std;

int cutRodUtil(vector<int> &price, int maxLen, int n, vector<vector<int>> &cost)
{
    // Base condition.
    if (n <= 0 || maxLen <= 0)
    {
        return 0;
    }

    // Checks whether problem is already calculated or not.
    if (cost[n][maxLen] != -1)
    {
        return cost[n][maxLen];
    }

    /*
       If the length of the rod to be cut is less than or equal
       to the size of rod of length 'max_len',
       then depending on profit, either it will accept the cut or discard it.
    */
    if (n <= maxLen)
    {
        cost[n][maxLen] = max(price[n - 1] + cutRodUtil(price, maxLen - n, n, cost), cutRodUtil(price, maxLen, n - 1, cost));
    }

    /*
       If the length of the rod to be cut is
       greater than the size of rod of length
       'max_len', cutting is not permitted.
    */
    else
    {
        cost[n][maxLen] = cutRodUtil(price, maxLen, n - 1, cost);
    }

    return cost[n][maxLen];
}

int cutRod(vector<int> &price, int n)
{
    // Two state dp to store the sub-problems.
    vector<vector<int>> cost(n + 2, vector<int>(n + 2, -1));
    
    return cutRodUtil(price, n, n, cost);
}

```



# Approach - III Bottom - up
```cpp

/*
    Time complexity = O(N ^ 2)
    Space complexity = O(N)

    Where 'N' is the length of the rod.
*/

int cutRod(vector<int> &price, int n)
{
    int cost[n + 1];
    cost[0] = 0;
    int i, j;

    for (i = 1; i <= n; i++)
    {
        int maxCost = INT_MIN;

        // Build the table in bottom up manner.
        for (j = 0; j < i; j++)
        {
            maxCost = max(maxCost, price[j] + cost[i - j - 1]);
        }

        // Contains maximum cost obtained from the rod of length 'i'.
        cost[i] = maxCost;
    }

    // Last entry conatins maximum cost obtained from the rod of length 'n'.
    return cost[n];
}

```


