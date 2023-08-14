# Symmetric Binary Tree

```md



```

# Approach - I
```cpp

/*
    Time complexity: O(N)
    Space complexity: O(H)

    where N is the number of nodes present in the tree.
    H is the height of the tree.
*/

bool checkSymmetricity(BinaryTreeNode<int>* firstRoot, BinaryTreeNode<int>* secondRoot)
{
    
    // Check if both nodes are NULL
    if(firstRoot == NULL && secondRoot == NULL)
    {
        return true;
    }

    // Check if one node is NULL, while the other is non-NULL
    if( (firstRoot == NULL && secondRoot != NULL) || (firstRoot != NULL && secondRoot == NULL) )
    {
        return false;
    }

    // Check if the number present in the nodes are unequal
    if(firstRoot->data != secondRoot->data)
    {
        return false;
    }

    
    // Finally, do the same for left node of firstRoot and right node of secondRoot, 
    // and right of firstRoot and left of secondRoot.
    return checkSymmetricity(firstRoot->right, secondRoot->left) && checkSymmetricity(firstRoot->left, secondRoot->right);
}

bool isSymmetric(BinaryTreeNode<int>* root)
{
    return checkSymmetricity(root, root); 
}

```

