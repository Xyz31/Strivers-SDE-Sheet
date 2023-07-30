# Boundary Traversal of Binary Tree


# Approach - I
```cpp

#include <bits/stdc++.h> 
/************************************************************

    Following is the Binary Tree node structure:
    
    template <typename T>
    class TreeNode {
        public :
        T data;
        TreeNode<T> *left;
        TreeNode<T> *right;

        TreeNode(T data) {
            this -> data = data;
            left = NULL;
            right = NULL;
        }

        ~TreeNode() {
            if(left)
                delete left;
            if(right)
                delete right;
        }
    };

************************************************************/

/*
Time Complexity: The optimized code has a time complexity of O(N), where N is the number of nodes in the binary tree. 
Each node is visited exactly once during the traversal.
Space Complexity: The space complexity is O(N) due to the space used by the result vector. 
In the worst case, the size of the result vector can be N, when all nodes are boundary nodes. 

Additionally, the recursive calls on the stack will use O(log N) space for a balanced binary tree and up to O(N) space for a skewed tree.
*/


// Function to check if a node is a leaf (has no left or right child)
bool isLeaf(TreeNode<int>* root){
    if(root->left == NULL && root->right == NULL){
        return true;
    }
    return false;
}

// Function to add the left boundary nodes to the result vector
void addLeftBoundary(TreeNode<int>* root , vector<int> &res){
    TreeNode<int>* curr = root->left;
    while(curr){
        if(isLeaf(curr) == false)
            res.push_back(curr->data);
        if(curr->left)
            curr = curr->left;
        else
            curr = curr->right;
    }
}

// Function to add the right boundary nodes to the result vector
void addRightBoundary(TreeNode<int>* root , vector<int> &res){
    TreeNode<int>* curr = root->right;
    stack<TreeNode<int>*> st;
    while(curr){
        if(isLeaf(curr) == false)
            st.push(curr);
        if(curr->right)
            curr = curr->right;
        else
            curr = curr->left;
    }
    while(!st.empty()){
        res.push_back(st.top()->data);
        st.pop();
    }
}

// Function to add the leaf nodes to the result vector
void addLeaves(TreeNode<int>* root , vector<int> &res){
    if(!root)
        return;
    if(isLeaf(root) == true){
        res.push_back(root->data);
        return;
    }
    if(root->left)
        addLeaves(root->left, res);
    if(root->right)
        addLeaves(root->right, res);
}

// Function to traverse the boundary of the binary tree and return the result vector
vector<int> traverseBoundary(TreeNode<int>* root){
    vector<int> res;
    if(!root)
        return res;
    if(isLeaf(root) == false){
        res.push_back(root->data);
    }
    addLeftBoundary(root, res);
    addLeaves(root, res);
    addRightBoundary(root, res);
    return res;
}


```