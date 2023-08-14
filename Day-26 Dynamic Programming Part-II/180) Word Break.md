# Word Break


```md



```
 

# Approach - I
```cpp

/*
    Time Complexity  : O(2 ^ N)
    Space Complexity : O(N)

    Where N is the length of target string.
*/

#include <unordered_set>

// Declare a hash map.
unordered_set < string > hashMap;

bool wordBreakHelper(string s) {

    // Len denotes size of current string.
    int len = s.size();

    // Base case.
    if (len == 0) {
        return true;
    }

    // Run a loop from 1 to length of target string.
    for (int i = 1; i <= len; i++) {
        /*
            If substring from 0 to i exist in hash map
            and remaining string recurs true then return true.
        */
        if (hashMap.find(s.substr(0, i)) != hashMap.end() and wordBreakHelper(s.substr(i, len - i))) {
            return true;
        }
    }

    // If no solution exist then return false.
    return false;
}

bool wordBreak(vector < string > & arr, int n, string & target) {
    // Clear hash map for current test case.
    hashMap.clear();

    // Insert all strings of a into hashmap.
    for (string s: arr) {
        hashMap.insert(s);
    }

    // Call wordBreakHelper to return answer.
    return wordBreakHelper(target);
}

```

# Approach - II Top-Down DP
```cpp

/*
    Time Complexity  : O(N ^ 2)
    Space Complexity : O(N)

    Where N is the length of target string.
*/

#include <unordered_set>

// Declare a hash map.
unordered_set < string > hashMap;

bool wordBreakHelper(string & s, int start, vector < int > & dp) {
    // Base case
    if (start == s.size()) {
        return dp[start] = 1;
    }

    // If result is already calculated then return it.
    if (dp[start] != -1) {
        return dp[start];
    }

    // Run a loop from 1 to length of target string.
    for (int i = start + 1; i <= s.size(); i++) {
        /*
            If substring from 0 to i exist in hash map
            And remaining string recurs true.
        */
        if (hashMap.find(s.substr(start, i - start)) != hashMap.end()) {
            if (wordBreakHelper(s, i, dp)) {
                return dp[start] = 1;
            }
        }
    }

    // If no solution exist then return false.
    return dp[start] = 0;
}

bool wordBreak(vector < string > & arr, int n, string & target) {
    // Clear hash map for current test case.
    hashMap.clear();

    // Insert all strings of a into hashmap.
    for (string s: arr) {
        hashMap.insert(s);
    }

    // Declare dp array and initialize all values with -1.
    vector < int > dp(target.size() + 1, -1);

    // Call wordBreakHelper to return answer.
    return wordBreakHelper(target, 0, dp);
}

```

# Approach - III Bottom-up DP
```cpp

/*
    Time Complexity  : O(N ^ 2)
    Space Complexity : O(N)

    Where N is the length of target string.
*/

#include <unordered_set>

bool wordBreak(vector < string > & arr, int n, string & target) {
    // Declare a hash map.
    unordered_set < string > hashMap;

    // Insert all strings of a into hashmap.
    for (string s: arr) {
        hashMap.insert(s);
    }

    // Declare dp array and initialize all values with false.
    vector < bool > dp(target.size() + 1, false);

    // Base case.
    dp[0] = true;

    // Run a loop from 1 to length of target string.
    for (int i = 1; i <= target.size(); ++i) {

        // Run a loop from i-1 to 0.
        for (int j = i - 1; j >= 0; --j) {

            // check only if a valid sequence of words (or a word) ends at j.
            if (dp[j]) {

                // Check if remaining string exist in hashmap.
                if (hashMap.find(target.substr(j, i - j)) != hashMap.end()) {

                    // Ending at i is a valid word So make dp[i] as true.
                    dp[i] = true;

                    // Break loop here because we have found a valid sequence ending here.
                    break;
                }
            }
        }
    }

    // Return dp[length of target].
    return dp[target.size()];
}

```