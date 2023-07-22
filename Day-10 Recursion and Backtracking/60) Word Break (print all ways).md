# Word Break (print all ways)


```cpp

#include <bits/stdc++.h> 
using namespace std;

vector<string> wordBreakUtil(string& s, unordered_set<string>& dictionary, unordered_map<string, vector<string>>& memo) {
    // If the result is already memoized, return it
    if (memo.find(s) != memo.end()) {
        return memo[s];
    }
    
    vector<string> result;
    
    // If the entire string is present in the dictionary, add it to the result
    if (dictionary.find(s) != dictionary.end()) {
        result.push_back(s);
    }
    
    // Break the string into different parts and recursively process them
    for (int i = 1; i < s.length(); i++) {
        string prefix = s.substr(0, i);
        
        // If the prefix is present in the dictionary, process the remaining string
        if (dictionary.find(prefix) != dictionary.end()) {
            string suffix = s.substr(i);
            vector<string> suffixResult = wordBreakUtil(suffix, dictionary, memo);
            
            // Append the prefix with each possible sentence from the suffix
            for (const string& sentence : suffixResult) {
                result.push_back(prefix + " " + sentence);
            }
        }
    }
    
    // Memoize the result and return it
    memo[s] = result;
    return result;
}

vector<string> wordBreak(string& s, vector<string>& dictionary) {
    unordered_set<string> dictSet(dictionary.begin(), dictionary.end());
    unordered_map<string, vector<string>> memo;
    return wordBreakUtil(s, dictSet, memo);
}


```