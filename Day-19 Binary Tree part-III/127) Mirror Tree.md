# Mirror Tree - Invert a Binary Tree

Approach Q-125
```md



```

# Approach - I
```cpp

#include <bits/stdc++.h> 
/************************************************************

    Following is the TreeNode class structure

    template <typename T>
    class TreeNode {
       public:
        T data;
        TreeNode<T> *left;
        TreeNode<T> *right;

        TreeNode(T data) {
            this->data = data;
            left = NULL;
            right = NULL;
        }
    };

************************************************************/



/*
TreeNode<int> *invertBinaryTree(TreeNode<int> *root, TreeNode<int> *leaf) {
    
    
    // write your code here.
}
*/


// T-O(N)
// S-O(Height)


/*
Helper function to find the leaf node in the binary tree and store the path in the stack.

Parameters:
- root: Pointer to the current node in the binary tree
- st: Reference to the stack to store the path
- leaf: Pointer to the leaf node to find

Returns:
- True if the leaf node is found, false otherwise
*/
bool helper(TreeNode<int>* root, std::stack<TreeNode<int>*>& st, TreeNode<int>* leaf){
    st.push(root);

    if(root->left == NULL && root->right == NULL){
        // Leaf node found
        if(root->data == leaf->data){
            return true;
        }
        else{
            st.pop();
            return false;
        }
    }

    bool left = false, right = false;

    if(root->left != NULL){
        // Recursively search the left subtree
        left = helper(root->left, st, leaf);
    }

    if(left){
        return true;
    }

    if(root->right != NULL){
        // Recursively search the right subtree
        right = helper(root->right, st, leaf);
    }

    if(right){
        return true;
    }

    // Remove the current node from the stack if the leaf node is not found in the subtree
    st.pop();
    return false;
}


/*
Function: invertBinaryTree
Reverses a binary tree with the given leaf node as the new root.

Parameters:
- root: Pointer to the root of the binary tree
- leaf: Pointer to the leaf node to be the new root

Returns:
- Pointer to the root of the inverted binary tree
*/
TreeNode<int>* invertBinaryTree(TreeNode<int>* root, TreeNode<int>* leaf){
    if(root == NULL){
        return root;
    } 

    std::stack<TreeNode<int>*> st;

    // Helper function to find the leaf node in the binary tree and store the path in the stack
    helper(root, st, leaf);

    TreeNode<int>* newRoot = st.top();
    st.pop();

    TreeNode<int>* parent = newRoot;

    // Traverse the stack to restructure the inverted binary tree
    while(!st.empty()){
        TreeNode<int>* curnode = st.top();
        st.pop();

        // If the current node is the left child of the parent, update the left pointer and swap the right and left children
        if(curnode->left == parent){
            curnode->left = NULL;
            parent->left = curnode;
        }
        else{
            // If the current node is the right child of the parent, swap the right and left children
            curnode->right = curnode->left;
            curnode->left = NULL;
            parent->left = curnode;
        }

        parent = parent->left;
    }

    return newRoot;
}




```

# Approach - II
```cpp



```