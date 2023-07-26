# Max width of a Binary Tree

# Approach - I
```cpp

#include <bits/stdc++.h> 
/************************************************************

    Following is the TreeNode class structure

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


// Function to find the maximum width of a binary tree
// Returns the maximum width among all the levels of the tree
// Time complexity: O(n), where n is the number of nodes in the binary tree
// Space complexity: O(m), where m is the maximum number of nodes at any level in the binary tree
int getMaxWidth(TreeNode<int> *root) {
    if (root == nullptr) {
        return 0;
    }
    
    int maxWidth = 0;
    
    queue<TreeNode<int>*> nodeQueue;
    nodeQueue.push(root);
    
    while (!nodeQueue.empty()) {
        int levelSize = nodeQueue.size();
        
        // Update the maximum width if the current level size is greater
        maxWidth = max(maxWidth, levelSize);
        
        for (int i = 0; i < levelSize; ++i) {
            TreeNode<int> *node = nodeQueue.front();
            nodeQueue.pop();
            
            if (node->left) {
                nodeQueue.push(node->left);
            }
            
            if (node->right) {
                nodeQueue.push(node->right);
            }
        }
    }
    
    return maxWidth;
}

```

# Approach - II
```cpp



```