# LFU cache

```md



```

```cpp

/*
    Time Complexity: O(M)
    Space Complexity: O(N)

    Where 'N' denotes size of cache and 'M' denotes the number of operations.
*/

#include <unordered_map>
#include <list>

struct Node {
    int key, value, cnt;
    Node* next;
    Node* prev;
    Node(int _key, int _value) : key(_key), value(_value), cnt(1), next(nullptr), prev(nullptr) {}
};

class LFUCache {
    int maxSizeCache;                       // Maximum capacity of the LFU cache
    int minFreq;                            // Minimum frequency of nodes in the cache
    int curSize;                            // Current number of nodes in the cache
    unordered_map<int, Node*> keyNode;      // Map to store key-node pairs for quick access
    unordered_map<int, list<Node*>> freqListMap; // Map to store frequency-list pairs

public:
    // Constructor to initialize the LFUCache with a given capacity
    LFUCache(int capacity) : maxSizeCache(capacity), minFreq(0), curSize(0) {}
    
    // Function to update the frequency list map when a node's frequency changes
    void updateFreqListMap(Node* node) {
        auto& freqList = freqListMap[node->cnt]; // Get the list of nodes with the same frequency
        freqList.erase(remove(freqList.begin(), freqList.end(), node), freqList.end());
        
        // If the current node had the minimum frequency and the list is empty, update the minFreq
        if (node->cnt == minFreq && freqList.empty()) {
            minFreq++;
        }
        
        node->cnt++; // Increment the frequency of the node
        freqListMap[node->cnt].push_front(node); // Add the node to the front of the list with the updated frequency
    }
    
    // Function to retrieve the value corresponding to a given key
    int get(int key) {
        if (keyNode.find(key) != keyNode.end()) { // Key found in the cache
            Node* node = keyNode[key];
            int val = node->value; // Retrieve the value
            updateFreqListMap(node); // Update the frequency list map for this node
            return val;
        }
        return -1; // Key not found in the cache
    }
    
    // Function to insert a key-value pair into the cache
    void put(int key, int value) {
        if (maxSizeCache == 0) {
            return;
        }
        
        if (keyNode.find(key) != keyNode.end()) { // Key already exists in the cache
            Node* node = keyNode[key];
            node->value = value; // Update the value of the existing node
            updateFreqListMap(node); // Update the frequency list map for this node
        } else {
            if (curSize == maxSizeCache) { // Cache is full, need to evict the least frequently used item
                auto& minFreqList = freqListMap[minFreq];
                Node* node = minFreqList.back(); // Get the least frequently used node
                keyNode.erase(node->key); // Remove the least frequently used key-node pair from the map
                minFreqList.pop_back(); // Remove the least frequently used node from the list
                curSize--;
            }
            
            Node* newNode = new Node(key, value); // Create a new node for the key-value pair
            keyNode[key] = newNode; // Add the key-node pair to the map
            freqListMap[1].push_front(newNode); // Add the new node to the front of the list with frequency 1
            minFreq = 1; // Update the minimum frequency to 1 since a new node is added
            curSize++; // Increment the current size of the cache
        }
    }
};


```