# Implement Trie ll


```md



```
 
```cpp

#include <bits/stdc++.h> 

/*
class Trie{

    public:

    Trie(){
        // Write your code here.
    }

    void insert(string &word){
        // Write your code here.
    }

    int countWordsEqualTo(string &word){
        // Write your code here.
    }

    int countWordsStartingWith(string &word){
        // Write your code here.
    }

    void erase(string &word){
        // Write your code here.
    }
};
*/



using namespace std;

class TrieNode {
public:
    TrieNode* children[26]; 
    // Array to store child nodes for each character ('a' to 'z')
    int wordCount; 
    // Number of words that end at this node
    
    TrieNode() {
        memset(children, 0, sizeof(children)); 
        // Initialize all child nodes to nullptr
        wordCount = 0; 
        // Initialize word count to 0
    }
};

class Trie {
private:
    TrieNode* root; 
    // Root node of the Trie
    
public:
    Trie() {
        root = new TrieNode(); 
        // Initialize the Trie with an empty root node
    }

    void insert(string& word) {
        TrieNode* curr = root;
        for (char c : word) {
            int index = c - 'a'; 
            // Compute the index of the character in the children array
            if (curr->children[index] == nullptr) {
                curr->children[index] = new TrieNode(); 
                // Create a new node if the character doesn't exist
            }
            curr = curr->children[index]; 
            // Move to the next node
        }
        curr->wordCount++; 
        // Increment the word count at the last node
    }

    int countWordsEqualTo(string& word) {
        TrieNode* curr = root;
        for (char c : word) {
            int index = c - 'a';
            if (curr->children[index] == nullptr) {
                return 0; 
                // Return 0 if the word doesn't exist
            }
            curr = curr->children[index];
        }
        return curr->wordCount; 
        // Return the word count at the last node
    }

    int countWordsStartingWith(string& prefix) {
        TrieNode* curr = root;
        for (char c : prefix) {
            int index = c - 'a';
            if (curr->children[index] == nullptr) {
                return 0; 
                // Return 0 if the prefix doesn't exist
            }
            curr = curr->children[index];
        }
        return countWords(curr); 
        // Recursively count words starting from the last node of the prefix
    }
    
    int countWords(TrieNode* node) {
        int count = node->wordCount;
        for (int i = 0; i < 26; i++) {
            if (node->children[i] != nullptr) {
                count += countWords(node->children[i]); 
                // Recursively count words in the subtree
            }
        }
        return count;
    }

    void erase(string& word) {
        TrieNode* curr = root;
        for (char c : word) {
            int index = c - 'a';
            if (curr->children[index] == nullptr) {
                return; 
                // Return if the word doesn't exist
            }
            curr = curr->children[index];
        }
        if (curr->wordCount > 0) {
            curr->wordCount--; 
            // Decrement the word count at the last node
        }
    }
};

```