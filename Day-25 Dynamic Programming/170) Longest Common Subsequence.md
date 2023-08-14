# Longest Common Subsequence


```md



```
 
# Approach - I Memoization
```cpp

/*
    Time Complexity : O(N * M)
    Space Complexity : O(N * M)
    where N and M are the lengths of str1 and str2 respectively.
*/

int lcsHelper(string str1, int n, string str2, int m, int **dp)
{
    // If the length of first string is zero, we don't have any common subsequence
    if (m == 0)
    {
        return 0;
    }

    // If the length of second string is zero, we don't have any common subsequence
    if (n == 0)
    {
        return 0;
    }

    // If already computed the answer for this state, we simply return it.
    if (dp[n - 1][m - 1] != -1)
    {
        return dp[n - 1][m - 1];
    }

    if (str1[n - 1] != str2[m - 1])
    {
        /*
            If the mth character of str1 is not equal to the nth character of str2,
            we return the maximum of answers obtained by
            1. Ignoring the nth character in the first string
            2. Ignoring the mth character in the second string
        */

        dp[n - 1][m - 1] = max(lcsHelper(str1, n - 1, str2, m, dp),
                               lcsHelper(str1, n, str2, m - 1, dp));
    }
    else
    {
        /*
            If the nth character of str1 is equal to the mth character of str2,
            this character will be included in the subsequence.
            Hence, we will add 1 to the length of lcs obtained
            removing the mth character from the first string and the
            nth character from the second string.
        */

        dp[n - 1][m - 1] = 1 + lcsHelper(str1, n - 1, str2, m - 1, dp);
    }

    return dp[n - 1][m - 1];
}

int lcs(string str1, string str2)
{
    int n = str1.length();
    int m = str2.length();
    int **dp = new int *[n];

    // Fill the dp Array with -1 which signifies none of the states have been computed.
    for (int i = 0; i < n; ++i)
    {
        dp[i] = new int[m];

        for (int j = 0; j < m; ++j)
        {
            dp[i][j] = -1;
        }
    }

    int ans = lcsHelper(str1, n, str2, m, dp);

    for(int i = 0; i < n; ++i)
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
    Time Complexity - O(N * M)
    Space Complexity - O(N * M)

    where N and M are the lengths of str1 and str2 respectively.
*/

int lcs(string str1, string str2)
{

    int m = str1.size();
    int n = str2.size();

    int **dp = new int *[m + 1];

    for (int i = 0; i <= m; i++)
    {
        dp[i] = new int[n + 1];
    }

    // First row
    for (int j = 0; j <= n; j++)
    {
        dp[0][j] = 0;
    }

    // First col
    for (int i = 0; i <= m; i++)
    {
        dp[i][0] = 0;
    }

    for (int i = 1; i <= m; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            if (str1[m - i] == str2[n - j])
            {
                dp[i][j] = 1 + dp[i - 1][j - 1];
            }
            else
            {
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
    }

    int ans = dp[m][n];

    for (int i = 0; i < m; ++i)
    {
        delete[] dp[i];
    }

    delete[] dp;

    return ans;
}

```

# Approach - II 2 Rows Approach
```cpp

/*
    Time Complexity : O(N * M)
    Space Complexity : O(N)

    where N and M are the lengths of strings str1 and str2 respectively
*/

int LCSHelper(string str1, int n, string str2, int m)
{
    int **dp = new int *[2];

    dp[0] = new int[m + 1];
    dp[1] = new int[m + 1];

    int currRowParity = 0;

    for (int i = 0; i <= n; i++)
    {
        currRowParity = i % 2;

        for (int j = 0; j <= m; j++)
        {
            if (i == 0 || j == 0)
            {
                dp[currRowParity][j] = 0;
            }
            else if (str1[i - 1] != str2[j - 1])
            {
                /*
                    If the ith character of str1 is not equal to the jth character of str2,
                    we return the maximum of answers obtained by
                    1. Ignoring the ith character in the first string
                    2. Ignoring the jth character in the second string
                */

                dp[currRowParity][j] =
                    max(dp[1 - currRowParity][j],
                        dp[currRowParity][j - 1]);
            }
            else
            {
                /*
                    If the ith character of str1 is equal to the nth character of str2,
                    this character will be included in the subsequence.
                    Hence, we will add 1 to the length of lcs obtained
                    removing the mth character from the first string and the
                    nth character from the second string.
                */
                dp[currRowParity][j] = dp[1 - currRowParity][j - 1] + 1;
            }
        }
    }

    int ans = dp[currRowParity][m];

    delete[] dp[0];
    delete[] dp[1];
    delete[] dp;

    return ans;
}

int lcs(string str1, string str2)
{
    return LCSHelper(str1, str1.length(), str2, str2.length());
}

```