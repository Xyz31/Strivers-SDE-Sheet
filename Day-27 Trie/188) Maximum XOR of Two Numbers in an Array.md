# Maximum XOR of Two Numbers in an Array



```md



```
 
```cpp

#include <bits/stdc++.h> 
/*
int maximumXor(vector<int> A)
{
    // Write your code here.   
}
*/


// Trie Node
struct TrieNode {
    TrieNode* children[2]; // Two children: 0 and 1
    TrieNode() {
        children[0] = nullptr;
        children[1] = nullptr;
    }
};

// Function to insert a number into the trie
void insertNumber(TrieNode* root, int number) {
    TrieNode* curr = root;
    
    // Traverse each bit of the number from left to right
    for (int i = 31; i >= 0; i--) {
        // Get the current bit
        int bit = (number >> i) & 1;
        
        // Create a new node if the current bit is not present
        if (curr->children[bit] == nullptr) {
            curr->children[bit] = new TrieNode();
        }
        
        // Move to the child node
        curr = curr->children[bit];
    }
}

// Function to find the maximum XOR value in the trie
int findMaxXOR(TrieNode* root, std::vector<int>& A) {
    int maxXOR = 0;
    
    // Traverse each number in the array
    for (int number : A) {
        TrieNode* curr = root;
        int currXOR = 0;
        
        // Traverse each bit of the number from left to right
        for (int i = 31; i >= 0; i--) {
            // Get the current bit
            int bit = (number >> i) & 1;
            
            // Check if the opposite bit is present in the trie
            if (curr->children[1 - bit] != nullptr) {
                currXOR |= (1 << i); // Update the current XOR value
                curr = curr->children[1 - bit]; // Move to the opposite bit node
            } else {
                curr = curr->children[bit]; // Move to the same bit node
            }
        }
        
        // Update the maximum XOR value
        maxXOR = std::max(maxXOR, currXOR);
    }
    
    return maxXOR;
}



// Function to calculate the maximum XOR value
int maximumXor(std::vector<int> A) {
    TrieNode* root = new TrieNode();
    
    // Insert each number into the trie
    for (int number : A) {
        insertNumber(root, number);
    }
    
    // Find the maximum XOR value in the trie
    int maxXOR = findMaxXOR(root, A);
    
    return maxXOR;
}


```