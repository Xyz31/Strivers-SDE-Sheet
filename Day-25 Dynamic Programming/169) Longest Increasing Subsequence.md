# Longest Increasing Subsequence


```md



```
 
# Approach - I
```cpp


/*
    Time Complexity : O(2 ^ N)
    Space Complexity : O(N)
    Where N is the size of the array
*/

#include <climits>

int longestIncreasingSubsequenceHelper(int arr[], int prev, int curPosition, int n)
{
    // Base case
    if (curPosition == n)
    {
        return 0;
    }

    int taken = 0;

    // Taking the current element
    if (arr[curPosition] > prev)
    {
        taken = 1 + longestIncreasingSubsequenceHelper(arr, arr[curPosition], curPosition + 1, n);
    }

    // Not Taking the current element
    int notTaken = longestIncreasingSubsequenceHelper(arr, prev, curPosition + 1, n);

    return max(taken, notTaken);
}
int longestIncreasingSubsequence(int arr[], int n)
{
    return longestIncreasingSubsequenceHelper(arr, INT_MIN, 0, n);
}

```

# Approach - II  Memoization
```cpp

/*
    Time Complexity : O(N ^ 2)
    Space Complexity : O(N ^ 2)
    Where N is the size of the array
*/

#include <climits>

int longestIncreasingSubsequenceHelper(int arr[], int prevPosition, int curPosition, int n, int **dp)
{
   
    // Base case.
    if (curPosition == n)
    {
        return 0;
    }
    
    // Already computed.
    if (dp[prevPosition + 1][curPosition] >= 0)
    {
        return dp[prevPosition + 1][curPosition];
    }

    int taken = 0;

    // Taking the current element.
    if (prevPosition < 0 || arr[curPosition] > arr[prevPosition])
    {
        taken = 1 + longestIncreasingSubsequenceHelper(arr, curPosition, curPosition + 1, n, dp);
    }

    // Not Taking the current element.
    int notTaken = longestIncreasingSubsequenceHelper(arr, prevPosition, curPosition + 1, n, dp);
    dp[prevPosition + 1][curPosition] = max(taken, notTaken);
    return dp[prevPosition + 1][curPosition];
}
int longestIncreasingSubsequence(int arr[], int n)
{

    int **dp = new int *[n + 1];
    for (int i = 0; i <= n; i++)
    {
        dp[i] = new int[n + 1];

        for (int j = 0; j <= n; j++)
        {
            dp[i][j] = -1;
        }
    }

    int ans = longestIncreasingSubsequenceHelper(arr, -1, 0, n, dp);

    for (int i = 0; i <= n; i++)
    {
        delete[] dp[i];
    }

    delete[] dp;
    return ans;
}


```


# Approach - II Iterative DP
```cpp

/*
    Time Complexity : O(N ^ 2)
    Space Complexity : O(N)
    Where N is the size of the array
*/

int longestIncreasingSubsequence(int arr[], int n)
{
    // dp[i] represents i+1'th length LIS ending at minimum integer dp[i]
    int dp[n]; 

    // Base case
    dp[0] = 1;

    int ans = 1;

    for (int i = 1; i < n; i++)
    {
        int maxval = 0;
        for (int j = 0; j < i; j++)
        {
            if (arr[i] > arr[j])
            {
                maxval = max(maxval, dp[j]);
            }
        }
        dp[i] = maxval + 1;
        ans = max(ans, dp[i]);
    }
    return ans;
}


```


# Approach - II Binary Search + DP
```cpp

/*
    Time Complexity : O(N * logN)
    Space Complexity : O(N)
    Where N is the size of the array
*/
#include <algorithm>
int longestIncreasingSubsequence(int arr[], int n)
{
    int dp[n]; // dp[i] represents i+1'th length LIS ending at minimum integer dp[i]
    int ans = 0;

    for (int i = 0; i < n; i++)
    {
        /*
            Since dp array stores elements in the sorted order therefore
            we can use binary search to find the correct position for
            arr[i] to be placed.
            And elements are present in the dp array from 0 to ans-1 position
            So we will be doing the binary search in this range.
        */
        int position = lower_bound(dp, dp + ans, arr[i]) - dp;
        dp[position] = arr[i];

        if (position == ans)
        {
            ans++;
        }
    }

    return ans;
}


```