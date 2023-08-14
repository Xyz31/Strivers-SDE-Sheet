# Reverse Words in a String

```md



```

```cpp



/*
T-O(N+M)
S-O(N)
*/

string reverseString(string &str) {
    vector<string> vs;  // Vector to store individual words
    string word = "";  // Temporary variable to store each word
    int n = str.length();  // Length of the input string
    
    // Loop through each character in the input string
    for (int i = 0; i < n; i++) {
        if (str[i] == ' ') {  // If a space is encountered, it indicates the end of a word
            vs.push_back(word);  // Add the word to the vector
            word = "";  // Reset the word variable for the next word
            
            // Skip consecutive spaces in the input string
            while (str[i] == ' ')
                i++;
            i--;  // Decrease i by 1 to account for the increment in the loop
        } else {
            word += str[i];  // Append the character to the word
        }
    }
    
    if (word != "")  // If there is a remaining word after the loop ends, add it to the vector
        vs.push_back(word);
    
    reverse(vs.begin(), vs.end());  // Reverse the vector containing the words
    
    string res = "";  // Result string to store the reversed words
    
    // Concatenate the reversed words with spaces
    for (auto x : vs) {
        res += x;
        res += " ";
    }
    
    return res;  // Return the reversed string
}

```