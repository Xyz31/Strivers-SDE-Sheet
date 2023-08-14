# Roman Number to Integer and vice versa

```md



```

```cpp

#include <map>
using namespace std;

// Function to convert a Roman numeral to an integer value
int romanToInt(string s) {
    // Create a map to store the Roman numeral characters and their corresponding integer values
    map<char, int> mp = { 
        { 'I', 1 },
        { 'V', 5 },
        { 'X', 10 },
        { 'L', 50 },
        { 'C', 100 },
        { 'D', 500 },
        { 'M', 1000 } 
    };

    int ans = 0; // Initialize the result (integer value) to 0
    int n = s.size(); // Get the length of the input Roman numeral string

    ans += mp[s[n - 1]]; // Add the value of the last character of the Roman numeral to the result

    // Loop through the Roman numeral characters from the second-to-last to the first character
    for (int i = n - 2; i >= 0; i--) {
        // If the value of the next character (to the right) is greater than the current character's value
        // It means it is a subtractive notation, e.g., IV (4), IX (9), XL (40), XC (90), etc.
        if (mp[s[i + 1]] > mp[s[i]]) {
            ans -= mp[s[i]]; // Subtract the current character's value from the result
        } else {
            ans += mp[s[i]]; // Otherwise, add the current character's value to the result
        }
    }

    return ans; // Return the final integer value of the Roman numeral
}


```

# Integer to Roman

```cpp


#include <bits/stdc++.h> 

// Function to convert an integer to its Roman numeral representation
string intToRoman(int num) {
    string result = ""; // Initialize an empty string to store the Roman numeral
    // Predefined vectors to store decimal values and their corresponding Roman numeral symbols
    vector<int> values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
    vector<string> symbols = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};

    // Loop through the vectors to construct the Roman numeral representation
    for (int i = 0; i < values.size(); i++) {
        while (num >= values[i]) { // Check if the current decimal value can be subtracted from the input number
            result += symbols[i]; // Append the corresponding Roman symbol to the result string
            num -= values[i]; // Reduce the input number by the subtracted decimal value
        }
    }
    return result; // Return the Roman numeral representation
} 


```