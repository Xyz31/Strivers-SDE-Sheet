# Check is a BT is BST or not


# Approach - I
```cpp

/*
    Time Complexity : O(N)
    Space Complexity : O(N).

    Where N denotes number of nodes in the binary tree
*/

bool helper(BinaryTreeNode<int>* root, int min, int max) {

    // An empty tree is a BST
    if (root == NULL) {
        return true;
    }

    // False if this node violates the min/max constraint
    if ((root->data < min) || (root->data > max)) {
        return false;
    }

    // Otherwise check the subtrees recursively, modifying the min or max constraint
    bool leftSearch = helper(root->left, min, root->data);
    bool rightSearch = helper(root->right, root->data, max);

    return leftSearch & rightSearch;
}

bool validateBST(BinaryTreeNode<int>* root) {
    return (helper(root, INT_MIN, INT_MAX));
}


```

# Approach - II Inorder Traversal

```cpp

/*
    Time Complexity : O(N)
    Space Complexity : O(N).
    
    Where N denotes number of nodes in the binary tree
*/

bool helper(BinaryTreeNode<int>* root, BinaryTreeNode<int>*& prev) {
    // Traverse the tree in inorder fashion
    // Keep track of previous node
    if (root) {
        if (!helper(root->left, prev)) {  // Check left subtree
            return false;
        }

        if (prev != NULL && root->data < prev->data)  // Traversal not in ascending order.
        {
            return false;
        }

        prev = root;

        return helper(root->right, prev);  // Check right subtree
    }

    return true;
}

bool validateBST(BinaryTreeNode<int>* root) {
    BinaryTreeNode<int>* prev = NULL;
    return (helper(root, prev));
}

```