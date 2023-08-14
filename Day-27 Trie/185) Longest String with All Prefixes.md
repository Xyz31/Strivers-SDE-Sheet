# Longest String with All Prefixes 
# Complete String


```md



```
 
```cpp

#include <bits/stdc++.h> 

/*
string completeString(int n, vector<string> &a){
    // Write your code here.
}
*/



#include <vector>
#include <string>
using namespace std;

/*
O(N * M^2), where N is the number of strings in the array and M is the maximum length of a string in the array.
S-O(1)
*/
string completeString(int n, vector<string> &a) {
    int maxLen = 0; 
    // Stores the maximum length of a complete string found so far
    string result; 
    // Stores the lexicographically smallest complete string found so far

    for (const string &str : a) { 
        // Iterate through each string in the array
        int len = str.length(); 
        // Get the length of the current string
        bool isValid = true; 
        // Flag to check if the string is a complete string

        for (int i = 1; i <= len; i++) { 
            // Iterate through each prefix of the string
            string prefix = str.substr(0, i); 
            // Get the prefix of the current length

            // Check if the prefix exists in the array
            if (find(a.begin(), a.end(), prefix) == a.end()) {
                isValid = false; 
                // Prefix not found, string is not a complete string
                break; 
                // No need to continue checking prefixes
            }
        }

        // If the string is a complete string and has a longer length or is lexicographically smaller than the current result
        if (isValid && (len > maxLen || (len == maxLen && str < result))) {
            maxLen = len; 
            // Update the maximum length
            result = str; 
            // Update the result string
        }
    }

    if (maxLen == 0) {
        return "None"; 
        // No complete string found
    } else {
        return result; 
        // Return the longest complete string
    }
}

```