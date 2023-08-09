# Palindrome Partitioning

Sample Input 1:
aaC


Sample Output 1:
["C", "a", "a"]
["C", "aa"]


Explanation For Input 1:
For the given string "aaC" there are two partitions in which all substring of partition is a palindrome.

## code
```cpp

#include <bits/stdc++.h> 


bool isPalindrome(int start, int end, string s) {
    while (start < end) {
        if (s[start] != s[end]) {
            return false;
        }
        start++, end--;
    }
    return true;
}

void solve(int ind, int n, string &s, vector<string> &path, vector<vector<string>> &ans) {
    if (ind == n) {
        ans.push_back(path); // Found a valid partition, add it to the result
        return;
    }

    for (int i = ind; i < n; i++) {
        if (isPalindrome(ind, i, s)) {
            path.push_back(s.substr(ind, i - ind+ 1)); // Add current palindrome substring to the path
            solve(i + 1, n, s, path, ans); // Recursively find partitions starting from the next index
            path.pop_back(); // Remove the current palindrome substring from the path to backtrack
        }
    }
}

vector<vector<string>> partition(string &s) {
    vector<string> path;
    vector<vector<string>> ans;
    solve(0, s.size(), s, path, ans); // Start the recursive partitioning from index 0
    return ans;
}

```