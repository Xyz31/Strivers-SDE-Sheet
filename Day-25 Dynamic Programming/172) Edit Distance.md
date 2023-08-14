# Edit Distance


```md



```
 
# Approach - I
```cpp

/*
    Time Complexity : O(3 ^ (N * M))
    Space Complexity : O(N + M)
    
    Where N is the size of first string and M is the size of second string.
*/

#include <algorithm>
#include <cstring>

int editDistanceHelper(int i, int j, string &str1, string &str2)
{
    // insert all characters of second string into first
    if (i == 0)
    {
        return j;
    }

    // If second string is empty, the only option is to
    // remove all characters of first string
    if (j == 0)
    {
        return i;
    }

    // If last characters are not same, consider all three
    // operations on last character of first string, recursively
    // compute minimum cost for all three operations and take
    // minimum of three values.
    int ans = 1 + min({
                      editDistanceHelper(i, j - 1, str1, str2),    // Insert
                      editDistanceHelper(i - 1, j, str1, str2),    // Remove
                      editDistanceHelper(i - 1, j - 1, str1, str2) // Replace
                  });

    // If last characters of two strings are same, nothing
    // much to do. Ignore last characters and get count for
    // remaining strings.
    if (str1[i - 1] == str2[j - 1])
    {
        ans = min(ans, editDistanceHelper(i - 1, j - 1, str1, str2));
    }
    return ans;
}

int editDistance(string str1, string str2)
{

    int n = str1.size() + 1, m = str2.size() + 1;

    int ans = editDistanceHelper(n, m, str1, str2);
  
    return ans;
}

```

# Approach - II Memoization
```cpp

/*
    Time Complexity : O(N * M)
    Space Complexity : O(N * M)
    Where N is the size of first string and M is the size of second string
*/
#include <algorithm>
#include <cstring>
int editDistanceHelper(int i, int j, string &str1, string &str2, int **dp)
{
    // insert all characters of second string into first
    if (i == 0)
    {
        return j;
    }

    // If second string is empty, the only option is to
    // remove all characters of first string
    if (j == 0)
    {
        return i;
    }

    if (dp[i][j] != -1)
    {
        return dp[i][j];
    }

    // If last characters are not same, consider all three
    // operations on last character of first string, recursively
    // compute minimum cost for all three operations and take
    // minimum of three values.
    int ans = 1 + min({
                      editDistanceHelper(i, j - 1, str1, str2, dp),    // Insert
                      editDistanceHelper(i - 1, j, str1, str2, dp),    // Remove
                      editDistanceHelper(i - 1, j - 1, str1, str2, dp) // Replace
                  });

    // If last characters of two strings are same, nothing
    // much to do. Ignore last characters and get count for
    // remaining strings.
    if (str1[i - 1] == str2[j - 1])
    {
        ans = min(ans, editDistanceHelper(i - 1, j - 1, str1, str2, dp));
    }
    dp[i][j] = ans;
    return ans;
}

int editDistance(string str1, string str2)
{

    int n = str1.size() + 1, m = str2.size() + 1;

    int **dp = new int *[n + 1];

    for (int i = 0; i <= n; i++)
    {
        dp[i] = new int[m + 1];

        for (int j = 0; j <= m; j++)
        {
            dp[i][j] = -1;
        }
    }

    int ans = editDistanceHelper(n, m, str1, str2, dp);
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
    Time Complexity : O(N * M)
    Space Complexity : O(N * M)
    Where N is the size of first string and M is the size of second string
*/

int editDistance(string str1, string str2)
{
	int n = str1.size(), m = str2.size();
	int **dp = new int *[n + 1];

	// dp[i][j] stores the edit distance of the i+1th length substring of str1 and
	// j+1th length substring of str2 starting from 0 index

	// dynamically allocate memory of size N for each row
	for (int i = 0; i <= n; i++)
	{
		dp[i] = new int[m + 1];
	}

	for (int i = 0; i <= n; i++)
	{
		for (int j = 0; j <= m; j++)
		{
			// If first string is empty, only option is to
			// insert all characters of second string considering other string of j length
			// so min operation would be j
			if (i == 0)
			{
				dp[i][j] = j;
			}

			else if (j == 0)
			{
				dp[i][j] = i;
			}

			// If last characters are same, then it doesnt cost anything
			else if (str1[i - 1] == str2[j - 1])
			{
				dp[i][j] = dp[i - 1][j - 1];
			}

			// If the last character is different, consider all
			// possibilities and find the minimum
			else
			{
				dp[i][j] = 1 + min(min(dp[i][j - 1],
									   dp[i - 1][j]),
								   dp[i - 1][j - 1]);
			}
		}
	}
	int ans = dp[n][m];

	//Clearing the dynamic array
	for (int i = 0; i <= n; i++)
	{
		delete[] dp[i];
	}

	delete[] dp;
	return ans;
}

```