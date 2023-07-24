# Longest Palindrome in a string


```cpp


string longestPalinSubstring(string s)
{
    // Write your code here.
    int n = s.size();
        if (n == 0) return "";

        vector<vector<int>> dp(n, vector<int>(n, 0));
        for (int i = 0; i < n; i++) { //  for length 1
            dp[i][i] = 1;
        }
        int start = 0, maxLength = 1, flag = 1;
        for (int i = 0; i < n; i++) { // for length 2
            if (s[i] == s[i + 1]) {
                dp[i][i + 1] = 1;
                if (flag) {
                    start = i;
                    maxLength = 2;
                    flag = 0;
                }
            }
        }
        // for length greater than 2
        for (int len = 3; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                int j = i + len - 1;
                if (s[i] == s[j] && dp[i + 1][j - 1]) {
                    dp[i][j] = 1;
                    if (len > maxLength) {
                        start = i;
                        maxLength = len;
                    }
                }
            }
        }
        return s.substr(start, maxLength);
}


```


# Optimization Explanation:

The optimized code uses Manacher's Algorithm to find the longest palindrome substring in linear time complexity. 
It preprocesses the input string by adding special characters between each character and at the ends to handle both even and odd-length palindromes. 
Then, it iterates through the processed string to calculate the lengths of the palindromic substrings centered at each position. 
Finally, it identifies the maximum length palindrome and returns the corresponding substring from the original input string.

The time complexity of the optimized code is O(n), where n is the length of the input string. 
This is because we only iterate through the processed string once to find the lengths of the palindromic substrings. 
The space complexity is O(n) as well, as we use an additional array of size n to store the lengths of the palindromic substrings.



```cpp

#include<vector>


#include <string>
#include <vector>

string preprocessString(const string& s) {
    // Function to preprocess the string by adding special characters between each character and at the ends
    int n = s.size();
    if (n == 0) return "^$";

    string processed = "^";
    for (int i = 0; i < n; i++) {
        processed += "#" + s.substr(i, 1);
    }
    processed += "#$";

    return processed;
}

string longestPalinSubstring(const string& s) {
    // Function to find the longest palindrome substring in the given string using Manacher's Algorithm

    string processed = preprocessString(s);
    int n = processed.size();
    vector<int> palinLengths(n, 0);  // Array to store the lengths of palindromic substrings
    int center = 0;  // Center of the current palindrome
    int right = 0;   // Rightmost boundary of the current palindrome

    for (int i = 1; i < n - 1; i++) {
        // Get the mirror index of 'i' with respect to the center
        int mirror = 2 * center - i;

        // Check if 'i' is within the current palindrome boundary
        if (i < right) {
            palinLengths[i] = std::min(right - i, palinLengths[mirror]);
        }

        // Expand around the current character to find the length of the palindrome centered at 'i'
        while (processed[i + 1 + palinLengths[i]] == processed[i - 1 - palinLengths[i]]) {
            palinLengths[i]++;
        }

        // Update the current palindrome boundary if necessary
        if (i + palinLengths[i] > right) {
            center = i;
            right = i + palinLengths[i];
        }
    }

    // Find the maximum length of a palindromic substring and its center index
    int maxLen = 0;
    int centerIndex = 0;
    for (int i = 1; i < n - 1; i++) {
        if (palinLengths[i] > maxLen) {
            maxLen = palinLengths[i];
            centerIndex = i;
        }
    }

    // Calculate the starting index of the longest palindrome substring in the original string
    int start = (centerIndex - maxLen - 1) / 2;

    return s.substr(start, maxLen);
}






```