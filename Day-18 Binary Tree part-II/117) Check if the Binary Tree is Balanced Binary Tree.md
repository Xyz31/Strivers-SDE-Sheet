# Check if the Binary Tree is Balanced Binary Tree


# Approach - I
```cpp

#include <bits/stdc++.h> 
/*************************************************************
 
    Following is the Binary Tree node structure

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

#define pii pair<int, int> // {height, isBalanced = bool}


/*
    Time complexity: O(N^2)
    Space complexity: O(N)
    
    Where 'N' is number of nodes in binary tree.
*/

pii balanced(BinaryTreeNode<int> *root) {
    // base case
    if(!root)
        return {0, 1};
    // recursive calls: postorder traversal
    pii left = balanced(root->left);
    pii right = balanced(root->right);
    // height of the current node
    int height = max(left.first, right.first) + 1;
    // is the current node balanced, same for left and right subtrees
    if(left.second && right.second && abs(left.first - right.first) <= 1)
        return {height, 1};
    else    
        return {height, 0};
}

bool isBalancedBT(BinaryTreeNode<int>* root) {
    // Write your code here.
    return balanced(root).second;
}



```

# Approach - II
```cpp

/*
    Time complexity: O(N)
    Space complexity: O(N)
    
    Where 'N' is number of nodes in binary tree.
*/

int helperMethod(BinaryTreeNode<int>* root){

    // Base case.
    if(!root){
        return 0;
    }

    int leftValue = helperMethod(root->left);
    int rightValue = helperMethod(root->right);

    // If one of them is '-1' then child subtree are not balanced.
    if(leftValue == -1 or rightValue == -1){
        return -1;
    }

    // Allow only '0, -1, 1' height differencein 'left' child subtree height and 'right' subtree height.
    if(abs(leftValue-rightValue) <= 1){
        return max(leftValue, rightValue)+1;
    }

    // If left and right child subtree height more than '2'.
    return -1;
}

bool isBalancedBT(BinaryTreeNode<int>* root){

    // Base condition.
    if(!root){
        return true;
    }

    // If root tree is balanced.
    if (helperMethod(root) != -1){
        return true;
    }
    else{
        return false;
    }
}

```