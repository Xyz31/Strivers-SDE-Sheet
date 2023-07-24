# Implement ATOI/STRSTR


```cpp

#include <bits/stdc++.h> 
int atoi(string str) {
    // Write your code here.
    int sign = 1; // Variable to store the sign of the number
    int i = 0; // Counter for iterating through the string
    int ans = 0; // Variable to store the converted integer
    if (str[i] == '-') {
        sign = -1; // If the string starts with '-', set the sign to -1
        i++;
    }
    for (; i < str.length(); i++) {
        if (str[i] - '0' >= 0 && str[i] - '0' <= 9) {
            ans = ans * 10 + str[i] - '0'; // Convert each character to its corresponding digit and add it to the answer
        }
    }
    return ans * sign; // Return the final converted integer with the appropriate sign
}


```