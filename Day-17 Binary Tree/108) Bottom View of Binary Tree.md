# Bottom View of Binary Tree

# Approach - I
```cpp

#include <bits/stdc++.h> 
/*************************************************************
 
    Following is the Binary Tree node structure.

    class BinaryTreeNode 
    {
    public : 
        T data;
        BinaryTreeNode<T> *left;
        BinaryTreeNode<T> *right;

        BinaryTreeNode(T data) {
            this -> data = data;
            left = NULL;
            right = NULL;
        }
    };

*************************************************************/


// Function to return the bottom view of a binary tree
vector<int> bottomView(BinaryTreeNode<int> *root) {

    vector<int> res;
    if (root == nullptr) return res;

    queue<pair<BinaryTreeNode<int>*, int>> q;  // Use explicit template argument for BinaryTreeNode
    map<int, int> mp;
    q.push({root, 0});

    while (!q.empty()) {
        auto tp = q.front();
        q.pop();

        BinaryTreeNode<int>* node = tp.first;  // Use explicit template argument for BinaryTreeNode
        int horrDist = tp.second;

        mp[horrDist] = node->data;

        if (node->left) q.push({node->left, horrDist - 1});
        if (node->right) q.push({node->right, horrDist + 1});
    }

    for (auto x : mp) {
        res.push_back(x.second);
    }

    return res;
}



```

# Approach - II
```cpp



```