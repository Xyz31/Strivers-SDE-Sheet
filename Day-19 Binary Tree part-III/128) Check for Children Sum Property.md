# Check for Children Sum Property


# Approach - I
```cpp

/*
    Time complexity : O(N^2)
    Space complexity : O(N)

    Where 'N' is the number of nodes.
*/

// Change child values.
void increment(BinaryTreeNode < int > * root, int diff) {
    if (root -> right != NULL) {
        root -> right -> data += diff;
        increment(root -> right, diff);
    } 
    else if (root -> left != NULL) {
        root -> left -> data += diff;
        increment(root -> left, diff);
    }

}

void change(BinaryTreeNode < int > * root) {

    // Base case.
    if (root == NULL || (root -> left == NULL && root -> right == NULL)) {
        return;
    }

    // Traverse substrees.
    change(root -> left);
    change(root -> right);

    // Child sum.
    int childVal = 0;
    if (root -> left != NULL) {
        childVal += root -> left -> data;
    }

    if (root -> right != NULL) {
        childVal += root -> right -> data;
    }

    int diff = childVal - root -> data;

    // childVal > parentVal
    if (diff > 0) {
        root -> data += diff;
    } 

    else {
        increment(root, -diff);
    }

}

void changeTree(BinaryTreeNode < int > * root) {
    change(root);
}

```

# Approach - II
```cpp

#include <bits/stdc++.h> 
/*************************************************************

    Following is the Binary Tree node structure

    class BinaryTreeNode
    {
    public :
        T data;
        BinaryTreeNode < T > *left;
        BinaryTreeNode < T > *right;

        BinaryTreeNode(T data) {
            this -> data = data;
            left = NULL;
            right = NULL;
        }
    };

*************************************************************/


/*
void changeTree(BinaryTreeNode < int > * root) {
    // Write your code here.
} 

*/


/**
 * Reorders the binary tree nodes based on the given conditions.
 * Time Complexity: O(N), where N is the number of nodes in the tree.
 * Space Complexity: O(N), considering the recursion stack for function calls.
 */
void reorder(BinaryTreeNode<int>* root) {
    if (root == NULL) return;

    int child = 0;
    if (root->left) {
        child += root->left->data;
    }
    if (root->right) {
        child += root->right->data;
    }

    if (child < root->data) {
        if (root->left) root->left->data = root->data;
        else if (root->right) root->right->data = root->data;
    }

    reorder(root->left);
    reorder(root->right);

    int tot = 0;
    if (root->left) tot += root->left->data;
    if (root->right) tot += root->right->data;
    if (root->left || root->right) root->data = tot;
}

/**
 * Changes the given binary tree by calling the reorder function.
 * Time Complexity: O(N), where N is the number of nodes in the tree.
 * Space Complexity: O(N), considering the recursion stack for function calls.
 */
void changeTree(BinaryTreeNode<int>* root) {
    reorder(root);
}

```