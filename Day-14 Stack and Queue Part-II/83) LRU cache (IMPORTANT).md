# LRU cache (IMPORTANT)


```cpp

/*
    Time Complexity: O(Q) 
    Space Complexity: O(capacity)
    
    where Q is the number of the given queries and 
    capacity is the maximum number of keys LRU Cache can store.
*/

#include<unordered_map>

class LRUCache {
public:
    // Define a class for the doubly linked list node
    class node {
    public:
        int key;
        int val;
        node* next;
        node* prev;
        node(int _key, int _val) {
            key = _key;
            val = _val;
        }
    };

    node* head = new node(-1, -1); // Create a sentinel node as the head of the list
    node* tail = new node(-1, -1); // Create a sentinel node as the tail of the list

    int cap; // Maximum capacity of the cache
    unordered_map<int, node*> m; // Map to store key-value pairs and corresponding node addresses

    // Constructor to initialize the cache
    LRUCache(int capacity) {
        cap = capacity;
        head->next = tail;
        tail->prev = head;
    }

    // Function to add a new node to the front of the list
    void addnode(node* newnode) {
        node* temp = head->next;
        newnode->next = temp;
        newnode->prev = head;
        head->next = newnode;
        temp->prev = newnode;
    }

    // Function to delete a node from the list
    void deletenode(node* delnode) {
        node* delprev = delnode->prev;
        node* delnext = delnode->next;
        delprev->next = delnext;
        delnext->prev = delprev;
    }

    // Function to retrieve the value corresponding to a given key
    int get(int key_) {
        if (m.find(key_) != m.end()) { // Key found in the cache
            node* resnode = m[key_];
            int res = resnode->val; // Retrieve the value
            m.erase(key_); // Remove the key-value pair from the map
            deletenode(resnode); // Remove the node from its current position
            addnode(resnode); // Move the node to the front of the list
            m[key_] = head->next; // Update the map with the new node address
            return res;
        }

        return -1; // Key not found in the cache
    }

    // Function to insert a key-value pair into the cache
    void put(int key_, int value) {
        if (m.find(key_) != m.end()) { // Key already exists in the cache
            node* existingnode = m[key_];
            m.erase(key_); // Remove the existing key-value pair from the map
            deletenode(existingnode); // Remove the existing node from the list
        }
        if (m.size() == cap) { // Cache is full, need to evict the least recently used item
            m.erase(tail->prev->key); // Remove the least recently used key-value pair from the map
            deletenode(tail->prev); // Remove the least recently used node from the list
        }

        addnode(new node(key_, value)); // Add the new key-value pair as a new node to the front of the list
        m[key_] = head->next; // Update the map with the new node address
    }
};


```