# Rabin Karp


```cpp

/*
    Time Complexity: O((n - m) * m)
    Space Complexity: O(1)

    Where 'n' and 'm' are the lengths of 'text' and 'pattern' respectively.
*/

vector<int> stringMatch(string text, string pattern)
{
    int n = text.size(), m = pattern.size();

    // List storing the indices of occurrences
    vector<int> ans;

    // Iterate through all possible starting indices
    for (int i = 0; i <= n - m; i++)
    {
        bool match = true;

        for (int j = 0; j < m; j++)
        {
            // If a character mismatch occurs
            if (text[i + j] != pattern[j])
            {
                match = false;
                break;
            }
        }

        if (match)
        {
            ans.push_back(i + 1);
        }
    }

    return ans;
}

```

# KMP Algo

```cpp

#include <iostream>
#include <vector>

// Function to build the prefix table for the pattern using the KMP algorithm
// The prefix table helps avoid unnecessary comparisons during pattern matching
vector<int> buildPrefixTable(const string& pattern) {
    int m = pattern.length(); // Length of the pattern
    vector<int> prefixTable(m); // Prefix table to store the longest proper prefix which is also a suffix

    int length = 0; // Length of the previous longest prefix suffix

    // Index i starts from 1, as the first character in the pattern doesn't have any proper prefix
    int i = 1;

    // Constructing the prefix table
    while (i < m) {
        if (pattern[i] == pattern[length]) {
            length++; // Increment length to include the current character in the prefix
            prefixTable[i] = length; // Store the length as the value for the current index
            i++; // Move to the next character in the pattern
        } else {
            if (length != 0) {
                // If there was a mismatch and we have a non-zero length prefix,
                // we update the length to the value in the prefix table at the previous index.
                length = prefixTable[length - 1];
            } else {
                // If there was a mismatch and the length is 0,
                // it means there is no proper prefix which is also a suffix.
                // So, we store 0 in the prefix table for the current index and move on.
                prefixTable[i] = 0;
                i++;
            }
        }
    }

    return prefixTable; // Return the constructed prefix table
}

// Function to find all occurrences of the pattern in the text using the KMP algorithm
vector<int> stringMatch(const string& text, const string& pattern) {
    vector<int> occurrences; // Vector to store the starting positions of occurrences in the text
    int n = text.length(); // Length of the text
    int m = pattern.length(); // Length of the pattern

    vector<int> prefixTable = buildPrefixTable(pattern); // Construct the prefix table for the pattern

    int i = 0; // Index for iterating through the text
    int j = 0; // Index for iterating through the pattern

    // Matching the pattern against the text
    while (i < n) {
        if (pattern[j] == text[i]) {
            j++; // If the characters match, move to the next character in the pattern
            i++; // Move to the next character in the text
        }

        if (j == m) {
            // If we reach the end of the pattern, it means we found a complete match.
            // So, we store the starting position of the match in the occurrences vector.
            occurrences.push_back(i - j + 1);

            // To find the next possible match, we update j using the prefix table.
            // The value at the last index of the prefix table represents the length of the longest proper prefix
            // that is also a suffix for the pattern. By moving j to that index, we avoid unnecessary comparisons.
            j = prefixTable[j - 1];
        } else if (i < n && pattern[j] != text[i]) {
            // If there is a mismatch and we have not reached the end of the text,
            // we update the j using the prefix table to move to the next possible matching position.
            // If j is 0, it means there is no possible proper prefix that matches the current position,
            // so we move to the next character in the text.
            if (j != 0) {
                j = prefixTable[j - 1];
            } else {
                i++;
            }
        }
    }

    return occurrences; // Return the vector containing the starting positions of occurrences
}

// The function stringMatch takes a text string and a pattern string as input
// and returns a vector containing the starting positions of all occurrences of the pattern in the text.
// The function uses the Knuth-Morris-Pratt (KMP) algorithm for more efficient string matching.


```