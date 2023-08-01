# 	Subset Sum


# Approach - I Recursion
```cpp

/*

    Time Complexity : O(2^N)
    Space Complexity : O(N)

    Where N is the number of elements in the array.

    
*/

int helper(vector < int > & arr, int n, int k) {
    // Base condition.
    if (n <= 0) {
        // If k = 0, we reached target sum.
        if (k == 0) {
            return 1;
        } else {
            return 0;
        }
    }

    // arr[n-1] not taken in considertion.   
    int x = helper(arr, n - 1, k);
    int y = 0;
    if(k - arr[n-1] >= 0){
        // arr[n-1] taken in considertion.
        y = helper(arr, n - 1, k - arr[n-1]);    
    }

    // Return current result.
    return x || y;
}

bool subsetSumToK(int n, int k, vector < int > & arr) {
    // Calling recursive function.
    int ans = helper(arr, n, k);
    if (ans == 1) {
        return true;
    } else {
        return false;
    }
}

```

# Approach - II Memoization
```cpp

/*

    Time Complexity : O(N * K)
    Space Complexity : O(N * K)

    Where N is the number of elements in the array and
    K is the target sum. 
    

*/

int helper(vector < int > & arr, int n, int k, vector < vector < int >> & memo) {
    // Base condition.
    if (n <= 0) {
        // If k = 0, we reached target sum.
        if (k == 0) {
            return 1;
        } else {
            return 0;
        }
    }

    // If memo[n][k] not equal to -1
    // then result of n,k already calculated.
    if (memo[n][k] != -1) {
        return memo[n][k];
    }


    // arr[n-1] not taken in considertion.   
    int x = helper(arr, n - 1, k, memo);
    int y = 0;
    if(k - arr[n-1] >= 0){
        // arr[n-1] taken in considertion.
        y = helper(arr, n - 1, k - arr[n-1], memo);    
    }

    // Store current result in memo.
    memo[n][k] = x || y;
    // Return current result.
    return memo[n][k];
}

bool subsetSumToK(int n, int k, vector < int > & arr) {
    // Declaring memo array and storing -1 in it:
    vector < vector < int >> memo(n+1, vector < int > (k+1, -1));
    // Calling recursive function.
    int ans = helper(arr, n, k, memo);

    if (ans == 1) {
        return true;
    } else {
        return false;
    }
}


```


# Approach - II Dynamic programming 
```cpp


/*

    Time Complexity : O(N * K)
    Space Complexity : O(N * K)

    Where N is the number of elements in the array and
    K is the target sum. 
    

*/

bool subsetSumToK(int n, int k, vector < int > & arr) {
    // Declaring dp array.
    vector < vector < bool >> dp(n + 1, vector < bool > (k + 1));

    // If required price = 0, answer always true.
    for (int i = 0; i <= n; i++) {
        dp[i][0] = true;
    }

    // If size of array = 0, answer always false.
    for (int i = 1; i <= k; i++) {
        dp[0][i] = false;
    }

    // Filling dp array.
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= k; j++) {
            dp[i][j] = dp[i - 1][j];
            if (arr[i - 1] <= j) {
                dp[i][j] = dp[i][j] || dp[i - 1][j - arr[i - 1]];
            }
        }
    }

    return dp[n][k];
}

```