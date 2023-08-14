# Palindrome Partitioning (MCM Variation)


```md



```
 
# Approach - I
```cpp

/*
    Time complexity: O(n * 2 ^ n)
    Space complexity: O(n ^ 2)

    Where 'n' is the length of the string.
*/

// Function to check if string str[i..j] is a palindrome or not
bool isPalindrome(string str, int i, int j)
{
    while (i <= j)
    {
        if (str[i++] != str[j--])
        {
            return false;
        }
    }
    return true;
}

/* Recursive function to find the minimum cuts needed in a string
   such that each partition is a palindrome */
int minPalinPartition(string str, int i, int j)
{
    /* Base case: if starting index i and ending index j are equal
       or str[i..j] is already a palindrome. */

    if (i == j || isPalindrome(str, i, j))
    {
        return 0;
    }

    // Stores minimum number cuts needed to partition str[i..j] intitally its infinite

    int min = INT_MAX;

    // Take the minimum over each possible position at which the String can be cut

    for (int k = i; k <= j - 1; k++)
    {
        // Recur to get minimum cuts required in str[i..k] and str[k+1..j]
        int count = 1 + minPalinPartition(str, i, k) + minPalinPartition(str, k + 1, j);
        // Update the min
        if (count < min)
        {
            min = count;
        }
    }

    // Return the minimum cuts required
    return min;
}

int palindromePartitioning(string str)
{
    int n = str.size();
    return minPalinPartition(str, 0, n - 1);
}

```

# Approach - II DP
```cpp

/*
    Time complexity: O(n ^ 3)
    Space complexity: O(n ^ 2)

    Where 'n' is the length of the string.
*/

int palindromePartitioning(string str)
{
    // Get the length of the string
    int n = str.length();

    /*
        Create two arrays to build the solution
        in bottom up manner
        cuts[i][j] = Minimum number of cuts needed for
        palindrome partitioning of substring str[i..j]
        isPalindrome[i][j] = true if substring str[i..j] is palindrome, else false
    */

    // cuts[i][j] is 0 if isPalindrome[i][j] is true
    int cuts[n][n];
    bool isPalindrome[n][n];

    // Every substring of length 1 is a palindrome
    for (int i = 0; i < n; i++)
    {
        isPalindrome[i][i] = true;
        cuts[i][i] = 0;
    }

    /*
        l is substring length. Build the solution in bottom up manner by
        considering all substrings of length starting from 2 to n.
    */
    for (int l = 2; l <= n; l++) 
    {
        /*
            For substring of length l, set
            different possible starting indexes
        */
        for (int i = 0; i < n - l + 1; i++)
        {
            int j = i + l - 1;  // Set ending index

            /*
                If l is 2, then we just need to
                compare two characters. Else
                need to check two corner characters
                and value of isPalindrome[i + 1][j - 1]
            */
            if (l == 2)
            {
                isPalindrome[i][j] = (str[i] == str[j]);
            }
            else
            {
                isPalindrome[i][j] = (str[i] == str[j]) && isPalindrome[i + 1][j - 1];
            }

            // If str[i..j] is palindrome, then cuts[i][j] is 0
            if (isPalindrome[i][j] == true)
            {
                cuts[i][j] = 0;
            }
            else
            {
                /*
                    Make a cut at every possible
                    location starting from i to j,
                    and get the minimum cost cut.
                */
                cuts[i][j] = INT_MAX;
                for (int k = i; k <= j - 1; k++)
                {
                    cuts[i][j] = min(cuts[i][j], cuts[i][k] + cuts[k + 1][j] + 1);
                }
            }
        }
    }

    // Return the min cut value for
    // complete string. i.e., str[0..n-1]
    return cuts[0][n - 1];
}

```


# Approach - III Higly Optimized DP
```cpp

/*
    Time complexity: O(n ^ 2)
    Space complexity: O(n ^ 2)

    Where 'n' is the length of the string.
*/

int palindromePartitioning(string str)
{
    // Get the length of the string
    int n = str.size();

    /* 
        isPalindrome[i][j] = true if substring str[i..j] is  palindrome, else false
        cuts[i][j] is 0 if isPalindrome[i][j] is true
    */

    int cuts[n];
    bool isPalindrome[n][n];

    int i, j, k, l;  // different looping variables

    // Every substring of length 1 is a palindrome
    for (i = 0; i < n; i++)
    {
        isPalindrome[i][i] = true;
    }

    /* 
        l is substring length. Build the solution in bottom up manner by
        considering all substrings of length starting from 2 to n.
    */
    for (l = 2; l <= n; l++)
    {
        // For substring of length l, set different possible starting indexes
        for (i = 0; i < n - l + 1; i++)
        {
            j = i + l - 1;  // Set ending index

            /*
                If l is 2, then we just need to compare two characters. Else need
                to check two corner characters and value of isPalindrome[i + 1][j - 1]
            */
            if (l == 2)
            {
                isPalindrome[i][j] = (str[i] == str[j]);
            }
            else
            {
                isPalindrome[i][j] = (str[i] == str[j]) && isPalindrome[i + 1][j - 1];
            }
        }
    }

    for (i = 0; i < n; i++)
    {
        if (isPalindrome[0][i] == true)
        {
            cuts[i] = 0;
        }
        else
        {
            cuts[i] = INT_MAX;
            for (j = 0; j < i; j++)
            {
                if (isPalindrome[j + 1][i] == true && 1 + cuts[j] < cuts[i]) cuts[i] = 1 + cuts[j];
            }
        }
    }

    // Return the min cut value for complete string. i.e., str[0..n-1]
    return cuts[n - 1];
}

```