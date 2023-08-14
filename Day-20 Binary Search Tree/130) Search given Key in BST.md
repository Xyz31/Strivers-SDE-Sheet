# Search given Key in BST


```md



```

# Approach - I Recursive Approach
```cpp

/*
    Time Complexity : O(H)
    Space Complexity : O(H)

    Where 'H' is the height of the given BST.
*/

bool searchInBST(BinaryTreeNode<int> *root, int x) {
    if(root == NULL) {
        return false;
    } else if(root->data == x) {
        return true;
    } else if(root->data < x) {
        // Recursively check for right subtree. 
        return searchInBST(root->right, x);
    } else {
        // Recursively check for left subtree. 
        return searchInBST(root->left, x);
    }
}

```

# Approach - II Iterative Approach
```cpp

/*
    Time Complexity : O(H)
    Space Complexity : O(1)

    Where 'H' is the height of the given BST.
*/

bool searchInBST(BinaryTreeNode<int> *root, int x) {
    BinaryTreeNode<int> *ptr = root;
    
    while(ptr != NULL) {
        if(ptr->data == x) {
            return true;
        } else if(ptr->data > x) {
            // Move 'ptr' to left child. 
            ptr = ptr->left;
        } else {
            // Move 'ptr' to left child. 
            ptr = ptr->right;   
        }
    }

    return false;
}

```