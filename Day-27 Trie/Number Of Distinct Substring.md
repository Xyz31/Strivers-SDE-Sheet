# Number Of Distinct Substring


```cpp

#include <bits/stdc++.h> 

/*
int distinctSubstring(string &word) {
    //  Write your code here.
}
*/


/*

1. Initialize a set to store distinct substrings.
2. Iterate over the word and consider each character as the starting point of a substring.
3. For each starting character, iterate over the remaining characters to form all possible substrings.
4. Add each substring to the set.
5. Finally, return the size of the set, which represents the number of distinct substrings.

*/

int distinctSubstring(std::string &word) {
    std::set<std::string> substrings;  
    // Set to store distinct substrings
    int n = word.length();  
    // Length of the input word

    // Iterate over each character as the starting point of a substring
    for (int i = 0; i < n; i++) {
        std::string substring = "";  
        // Current substring
        for (int j = i; j < n; j++) {
            substring += word[j];  
            // Append current character to the substring
            substrings.insert(substring);  
            // Add the substring to the set
        }
    }

    return substrings.size();  
    // Return the number of distinct substrings
}


```