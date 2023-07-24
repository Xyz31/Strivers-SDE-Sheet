# Check for Anagrams


```cpp

#include <bits/stdc++.h> 

/*
bool areAnagram(string &str1, string &str2){
    // Write your code here.
}
*/


bool areAnagram(string &str1, string &str2) {
    // Lengths of the strings must be the same for them to be anagrams
    if (str1.length() != str2.length()) {
        return false;
    }

    // Create a frequency array to store the count of each character
    int freq[26] = {0}; // Assuming input consists of lowercase alphabets only

    // Increment the count of characters in the first string
    for (char c : str1) {
        freq[c - 'a']++;
    }

    // Decrement the count of characters in the second string
    for (char c : str2) {
        freq[c - 'a']--;
    }

    // Check if all character frequencies are zero
    for (int i = 0; i < 26; i++) {
        if (freq[i] != 0) {
            return false;
        }
    }

    // All character frequencies are zero, so the strings are anagrams
    return true;
}

```