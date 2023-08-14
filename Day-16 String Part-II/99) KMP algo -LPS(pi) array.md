# KMP algo / LPS(pi) array

```md



```

```cpp

#include <bits/stdc++.h> 

/*
bool findPattern(string p, string s)
{
    // Write your code here.
}
*/


/*
Note: The find function returns the position of the first occurrence of the substring 'p' in 's'. 
If 'p' is not found, it returns string::npos.
*/

bool findPattern(string p, string s)
{
    // Find the first occurrence of p in s
    size_t found = s.find(p);

    // If found is not equal to string::npos, it means p is present in s
    if (found != string::npos)
        return true;

    // If p is not found, return false
    return false;
}

```

# KMP

```cpp

/*
    Time complexity: O(N)
    Space complexity: O(M)

    Where N is the length of string s and M is length of string p.
*/

// Function to get the LPS.
void getLps(string p, vector<int> &lps) 
{
    int len = 0;
    int index = 1;
    int m = p.size();

    while (index < m)
    {
        if (p[index] == p[len])
        {
            len += 1;
            lps[index] = len;
            index += 1;
        }

        else
        {
            if (len == 0)
            {
                lps[index] = 0;
                index += 1;
            }

            else
            {
                // Skipping the characters.
                len = lps[len - 1]; 
            }
        }
    }
}

bool findPattern(string p, string s)
{
    int m = p.size();
    int n = s.size();
    vector<int> lps(m, 0);

    getLps(p, lps);

    // We will use these indices to traverse in s and p.
    int index1 = 0;
    int index2 = 0;

    while (index1 < n)
    {
        if (s[index1] == p[index2])
        {
            index2++;
            index1++;
            if (index2 == m)
            {
                return true;
            }

            if (index1 == n)
            {
                return false;
            }
        }
        else
        {
            if (index2 == 0)
            {
                index1 += 1;
            }
            else
            {
                // Skipping the characters.
                index2 = lps[index2 - 1];
            }
        }
    }

    return false;
}

```