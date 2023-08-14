# Predecessor And Successor In BST

```md



```


# Approach - I INORDER TRAVERSAL
```cpp

/*
    Time Complexity : O(N)
    Space Complexity : O(N)

    where 'N' is the number of nodes in the BST.
*/

void inorder(BinaryTreeNode<int> *root, vector<int> &inorderArray)
{
    if (root == NULL)
    {
        return;
    }

    inorder(root->left, inorderArray);

    inorderArray.push_back(root->data);

    inorder(root->right, inorderArray);
}

pair<int, int> predecessorSuccessor(BinaryTreeNode<int> *root, int key)
{
    // To store the inorder traversal of the BST.
    vector<int> inorderArray;

    inorder(root, inorderArray);

    int predecessor = -1, successor = -1;

    for (int i = 0; i < inorderArray.size(); i++)
    {
        if (inorderArray[i] == key)
        {
            // If predecessor exist.
            if (i - 1 >= 0)
            {
                predecessor = inorderArray[i - 1];
            }

            // If successor exist.
            if (i + 1 < inorderArray.size())
            {
                successor = inorderArray[i + 1];
            }
            break;
        }
    }

    return {predecessor, successor};
}

```

# Approach - II OPTIMIZED APPROACH

```cpp

/*
    Time Complexity : O(N)
    Space Complexity : O(1)

    where 'N' is the number of nodes in the BST.
*/

pair<int, int> predecessorSuccessor(BinaryTreeNode<int>* root, int key)
{
    int predecessor = -1;
    int successor = -1;

    // Reach to the key.
    while (root -> data != key)
    {
        if (key > root -> data)
        {
            predecessor = root -> data;
            root = root -> right;
        }
        else
        {
            successor = root -> data;
            root = root -> left;
        }
    }

    
    BinaryTreeNode<int>* rightSubtree = root -> right;

    while (rightSubtree != NULL)
    {
        successor = rightSubtree -> data;
        rightSubtree = rightSubtree -> left;
    }


    BinaryTreeNode<int>* leftSubtree = root -> left;

    while (leftSubtree != NULL)
    {
        predecessor = leftSubtree -> data;
        leftSubtree = leftSubtree -> right;
    }

    return {predecessor, successor};
}

```