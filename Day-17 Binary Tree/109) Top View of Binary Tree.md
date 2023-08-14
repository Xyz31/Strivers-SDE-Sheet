# Top View of Binary Tree

```md



```


# Approach - I
```cpp

#include <bits/stdc++.h> 
/************************************************************

    Following is the TreeNode class structure:

    template <typename T>
    class TreeNode {
       public:
        T val;
        TreeNode<T> *left;
        TreeNode<T> *right;

        TreeNode(T val) {
            this->val = val;
            left = NULL;
            right = NULL;
        }
    };

************************************************************/


/*
 The time complexity of the code is O(n) and 
 the space complexity is O(n), where n is the number of nodes in the tree.
*/

vector<int> getTopView(TreeNode<int> *root) {
    // Write your code here.
    vector<int> res;
    if (root == nullptr) return res; // If the root is NULL, return the empty vector

queue<pair<TreeNode<int>*, int>> q; // Create a queue to perform level order traversal
map<int, int> mp; // Create a map to store the horizontal distance and corresponding node value

q.push({ root, 0 }); // Push the root node with horizontal distance 0 into the queue

while (!q.empty()) {
    auto tp = q.front();
    q.pop();

    TreeNode<int>* node = tp.first;
    int horrDist = tp.second;

    if (mp.count(horrDist) == 0)
        mp[horrDist] = node->val; // Store the node value in the map if the horizontal distance is encountered for the first time

    if (node->left) q.push({ node->left, horrDist - 1 }); // Push the left child with a horizontal distance decremented by 1
    if (node->right) q.push({ node->right, horrDist + 1 }); // Push the right child with a horizontal distance incremented by 1
}

for (auto x : mp) {
    res.push_back(x.second); // Push the node values from the map into the result vector
}

return res; // Return the top view elements

}

```

# Approach - II
```cpp



```