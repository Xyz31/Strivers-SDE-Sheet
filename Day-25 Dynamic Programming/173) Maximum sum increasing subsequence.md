# Maximum sum increasing subsequence


```md



```
 
# Approach - I Recursion
```cpp

/* 
    Time Complexity : O(N ^ N)
    Space Complexity : O(N)

     Where N is the number of dumbbells in RACK.
*/


int maxIncreasingDumbbellsSumUtil(vector<int> &rack, int n, int &totalWeight)
{
    // Base case.
    if(n == 0)
    {
        return 0;
    }

    int currWeight = rack[n - 1];

    for(int i = 1 ; i < n ; i++)
    {
        int temp = maxIncreasingDumbbellsSumUtil(rack, i, totalWeight);
        // Choose element which is smaller than last element.
        if(rack[i - 1] < rack[n - 1] && temp + rack[n - 1] > currWeight)
        {
            currWeight = temp + rack[n - 1];
        }
    }

    // Store the maximum weigth in 'totalWeight'.
    if(currWeight > totalWeight)
    {
        totalWeight = currWeight;
    }

    return currWeight;
}


int maxIncreasingDumbbellsSum(vector<int> &rack, int n)
{
    if(n == 1)
    {
        return rack[n - 1];
    }
    
    int totalWeight = INT_MIN;

    maxIncreasingDumbbellsSumUtil(rack, n, totalWeight);

    return totalWeight;
}


```

# Approach - II Memoization
```cpp

/*  
    Time Complexity : O(N ^ 2)
    Space Complexity : O(N)

    Where N is the number of dumbbells in RACK

*/

int maxIncreasingDumbbellsSumUtil(vector<int> &rack, int n, int &totalWeight, vector<int> &lookUp)
{
    // Base case.
    if(n == 0)
    {
        return 0;
    }
    
    // Check for already calculated result.
    if(lookUp[n - 1] != -1)
    {
        return lookUp[n - 1];
    }

    int currWeight = rack[n - 1];
    
    for(int i = 1; i < n; i++)
    {
        int temp = maxIncreasingDumbbellsSumUtil(rack, i, totalWeight, lookUp);

        // Choose element which is smaller than last element.
        if(rack[i - 1] < rack[n - 1] && temp + rack[n - 1] > currWeight)
        {
            currWeight = temp + rack[n - 1];
        }
    }

    // Store the maximum weigth in 'totalWeight'.
    if(currWeight > totalWeight)
    {
        totalWeight = currWeight;
    }
  
    return lookUp[n - 1] = currWeight;
}


int maxIncreasingDumbbellsSum(vector<int> &rack, int n)
{
    if(n == 1)
    {
        return rack[n - 1];
    }
    
    vector<int> lookUp(n, -1);
    
    int totalWeight = INT_MIN;

    maxIncreasingDumbbellsSumUtil(rack, n, totalWeight, lookUp);

    return totalWeight;
}



```

# Approach - II Dynamic Programming
```cpp

/*
    Time Complexity : O(N ^ 2)
    Space Complexity : O(N)

    Where N is the number of Dumbbells in RACK
*/


int maxIncreasingDumbbellsSum(vector<int> &rack, int n)
{
    int dp[n];
    int totalWeight = INT_MIN;

    for(int i = 0; i < n; i++)
    {
        dp[i] = rack[i];
    }

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < i; j++)
        {
            // Choose element which is smaller than last element.
            if(rack[i] > rack[j] && dp[i] < dp[j] + rack[i])
            {
                dp[i] = dp[j] + rack[i];
            }
        }

        // Store the maximum weigth in 'totalWeight'.
        totalWeight = max(totalWeight, dp[i]);
    }

    return totalWeight;
}


```