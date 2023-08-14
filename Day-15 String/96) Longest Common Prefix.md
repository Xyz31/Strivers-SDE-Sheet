# Longest Common Prefix 

```md



```

```cpp

#include<algorithm>
using namespace std;

// Function to find the longest common prefix among a vector of strings
string longestCommonPrefix(vector<string> &strs, int n)
{
    // Write your code here
    
    // Initialize the longest common prefix (lcp) with the first string in the vector
    string lcp = strs[0];

    // Loop through the remaining strings in the vector starting from the second string
    for(int i = 1; i < n; i++){
        int j = 0; // Initialize a pointer for iterating through characters of lcp and the current string
        string temp = ""; // Temporary string to store the new common prefix for the current string

        // Continue looping until we reach the end of either the lcp or the current string
        while(lcp[j] != '\0' && strs[i][j] != '\0'){
            // If the character at the same position in lcp and the current string is not the same,
            // it means we have found the maximum common prefix for the current string,
            // and we update the lcp to be the temporary string (the common prefix found so far).
            if(lcp[j] != strs[i][j]){
                lcp = temp;
                break;
            }
            // If the characters are the same, add the character to the temporary string
            temp += strs[i][j];
            j++; // Move to the next character in lcp and the current string
        }
    }

    // Return the final longest common prefix found among all the strings
    return lcp;
}


```