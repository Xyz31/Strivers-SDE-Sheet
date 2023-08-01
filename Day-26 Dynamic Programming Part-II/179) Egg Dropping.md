# Egg Dropping



# Cut Logs

# Approach - I Recursion
```cpp

/*
    Time Complexity: O(K ^ N)
    Space Complexity: O(N + K)

    Where K is the number of axes and N is capacity of log cutting stand.
*/

int cutLogs(int k, int n)
{
    // Check if N or K is less than 1
    if(n <= 1 || k <= 1)
    {
        return n;
    }

    int ans = n;
	
    // Iterate i from 1 to N + 1
    for(int i=1; i <= n; i++)
    {
        int cur = max( cutLogs(k-1, i-1), cutLogs(k, n-i) );
        
        // Update ans with minimum of ans and cur
        ans = min(ans, cur);
    }

    return ans + 1;
}



```

# Approach - II Memoization
```cpp

/*
    Time Complexity: O(K * N * N)
    Space Complexity: O(K * N)

    Where K is the number of axes and N is capacity of log cutting stand.
*/

#include <vector>

int cutLogsHelper(int k, int n, vector<vector<int>> &lookUp)
{	
    // Check if N or K is less than 1
    if(n <= 1 || k <= 1)
    {
        return n;
    }

    if(lookUp[k][n] != -1)
    {
        return lookUp[k][n];
    }

    int ans = n;
	
    // Iterate i from 1 to N + 1
    for(int i=1; i <= n; i++)
    {
        int cur = max( cutLogsHelper(k-1, i-1, lookUp), cutLogsHelper(k, n-i, lookUp) );
        
        // Update ans with minimum of ans and cur
        ans = min(ans, cur);
    }
	
    // Store the answer in lookUp
    lookUp[k][n] = ans + 1;

    return lookUp[k][n];
}

int cutLogs(int k, int n)
{	
    // Create an array lookUp
    vector<vector<int>> lookUp(k + 1, vector<int>(n + 1, -1));

    return cutLogsHelper(k, n, lookUp);
}



```


# Approach - III Dynamic Programming
```cpp

/*
    Time Complexity: O(K * N * N)
    Space Complexity: O(K * N)

    Where K is the number of axes and N is capacity of log cutting stand.
*/

int cutLogs(int k, int n)
{	
    // Create an array dp
    int dp[k + 1][n + 1];

    for(int i=0; i <= k; i++)
    {
        for(int j=0; j <= n; j++)
        {
            dp[i][j] = j;
        }
    }
	
    // Iterate i from 2 to K
    for(int i=2; i <= k; i++)
    {	
        // Iterate j from 2 to N
        for(int j=2; j <= n; j++)
        {
            for(int t=1; t <= j; t++)
            {
                int cur = max( dp[i-1][t-1], dp[i][j-t] );
                dp[i][j] = min(dp[i][j], cur);
            }
            
            // Increment dp[i][j] by 1
            dp[i][j]++;
        }
    }
	
    // Return the element dp[k][n]
    return dp[k][n];
}



```


# Approach - IV Optimized DP
```cpp

/*
    Time Complexity: O(K * N)
    Space Complexity: O(N)

    Where K is the number of axes and N is capacity of log cutting stand.
*/

#include <vector>

int cutLogs(int k, int n)
{	
    // Create an array dp
    vector<int> dp(n + 1);

    for(int i=0; i <= n; i++)
    {
        dp[i] = i;
    }
	
    // Iterate i from 2 to K
    for(int i=2; i <= k; i++)
    {	
        // Create an array dp2
        vector<int> dp2(n + 1);
        int t = 1;
		
        // Iterate j from 1 to N
        for(int j=1; j <= n; j++)
        {
            while(t < j and max(dp[t - 1], dp2[j - t]) > max(dp[t], dp2[j - t - 1]))
            {
                t++;
            }
            dp2[j] = 1 + max(dp[t - 1], dp2[j - t]);
        }
		
        // Update dp with dp2
        dp = dp2;
    }
	
    // Return the element dp[n]
    return dp[n];
}



```


# Approach - V Pre Computation
```cpp


/*
    Time Complexity: O(N ^ 1/3 + T * logN)
    Space Complexity: O(N ^ 1/3)

    Where N is capacity of log cutting stand.
*/

#include <vector>
#include <cmath>

// Create an array dp
vector<vector<int>> dp(15, vector<int>(1, 0));

void preComp()
{
    for(int i=0; 1; i++)
    {
        int cur = dp[3][i] + (i*(i+1))/2 + 1;
        dp[3].push_back(cur);
		
        // Check if cur is greater than 10000
        if(cur > 10000)
        {
            break;
        }
    }
	
    // Iterate i from 4 to 14
    for(int i=4; i <= 14; i++)
    {
        for(int j=0; 1; j++)
        {
            int cur = dp[i][j] + dp[i-1][j] + 1;
            dp[i].push_back(cur);
			
            // Check if cur is greater than 10000
            if(cur > 10000)
            {
                break;
            }
        }
    }
}

int cutLogs(int k, int n)
{	
    // Check if K is equal to 1
    if(k == 1)
    {
        return n;
    }
	
    // Check if K is equal to 2
    if(k == 2)
    {
        return ceil((-1.0 + sqrt(1 + 8 * n)) / 2.0);
    }

    if(dp[3].size() == 1)
    {
        preComp();
    }
	
    // Update K with minimum value of K and 14
    k = min(k, 14);
	
    // Find the lower bound
    int ans = lower_bound(dp[k].begin(), dp[k].end(), n) - dp[k].begin();
    return ans;
}


```
