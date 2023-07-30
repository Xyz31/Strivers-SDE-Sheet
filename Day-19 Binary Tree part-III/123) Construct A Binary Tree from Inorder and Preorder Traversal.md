# Construct A Binary Tree from Inorder and Preorder Traversal


# Approach - I
```cpp

/*
    Time Complexity : O(N^2)
    Space Complexity : O(N)

    Where 'N' is the number of nodes in the given binary tree.
*/

// Constructs the subtree and returns the root node.
TreeNode<int> *constructTree(int inStart, int inEnd, int &pIndex, vector<int> &inorder, vector<int> &preorder)
{
    if (inStart > inEnd)
    {
        // Subtree is empty.
        return NULL;
    }

    // Get root node value from preorder sequence.
    int rootNode = preorder[pIndex];

    // Increment the index denoting the first element of preorder traversal.
    pIndex = pIndex + 1;

    // Create the root node with "rootNode" value.
    TreeNode<int> *root = new TreeNode<int>(rootNode);

    if (inStart == inEnd)
    {
        // There is a single node in the given subtree.
        return root;
    }
    else
    {
        // Get the index of root node from the inorder sequence.
        int inIndex;
        for (int i = inStart; i <= inEnd; i++)
        {
            if (rootNode == inorder[i])
            {
                // Root node value found.
                inIndex = i;
                break;
            }
        }

        // Recur for the left subtree.
        TreeNode<int> *leftChild = constructTree(inStart, inIndex - 1, pIndex, inorder, preorder);

        // Recur for the right subtree.
        TreeNode<int> *rightChild = constructTree(inIndex + 1, inEnd, pIndex, inorder, preorder);

        // Link the left and right child to the root node.
        root->left = leftChild;
        root->right = rightChild;

        return root;
    }
}

TreeNode<int> *buildBinaryTree(vector<int> &inorder, vector<int> &preorder)
{

    // Index of the first element of the preorder sequence
    int pIndex = 0;

    return constructTree(0, inorder.size() - 1, pIndex, inorder, preorder);
}

```

# Approach - II
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

/**/

/*
    Time Complexity : O(N)
    Space Complexity : O(N)

    Where 'N' is the number of nodes in the given binary tree.
*/
// Helper function to build a binary tree from given preorder and inorder traversals
TreeNode<int>* buildTreeHelp(vector<int>& preorder, int preStart, int preEnd, vector<int>& inorder, int inStart, int inEnd, map<int, int>& inorderMap)
{
    // Base case: Empty subtree
    if (preStart > preEnd || inStart > inEnd) {
        return NULL;
    }

    // Create a new node with the value from the current preorder index
    TreeNode<int>* root = new TreeNode<int>(preorder[preStart]);

    // Find the index of the root value in the inorder traversal
    int inorderIndex = inorderMap[preorder[preStart]];

    // Calculate the size of the left subtree
    int leftSize = inorderIndex - inStart;

    // Recursively build the left and right subtrees
    // Pass the updated indices and the inorder map
    root->left = buildTreeHelp(preorder, preStart + 1, preStart + leftSize, inorder, inStart, inorderIndex - 1, inorderMap);
    root->right = buildTreeHelp(preorder, preStart + leftSize + 1, preEnd, inorder, inorderIndex + 1, inEnd, inorderMap);

    // Return the constructed tree
    return root;
}

// Function to build a binary tree from given inorder and preorder traversals
TreeNode<int> *buildBinaryTree(vector<int> &inorder, vector<int> &preorder)
{
    // Create a map to store the indices of inorder values
    map<int, int> inMap;
    for (int i = 0; i < inorder.size(); i++) {
        inMap[inorder[i]] = i;
    }

    // Set the initial indices for the helper function
    int preStart = 0, preEnd = preorder.size() - 1;
    int inStart = 0, inEnd = inorder.size() - 1;

    // Call the helper function to build the binary tree
    TreeNode<int>* root = buildTreeHelp(preorder, preStart, preEnd, inorder, inStart, inEnd, inMap);

    // Return the root of the constructed binary tree
    return root;
}


```