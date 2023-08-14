# Diameter of Binary Tree

```md



```

# Approach - I
```cpp

/*
    Time Complexity : O(N^2)
    Space Complexity : O(N)
	
    Where 'N' is the number of nodes in the given binary tree.
*/

int getHeight(TreeNode<int> *root)
{
    if (root == NULL)
    {
        // Height of empty tree is 0.
        return 0;
    }

    // Get the height of left subtree.
    int leftHeight = getHeight(root->left);

    // Get the height of right subtree.
    int rightHeight = getHeight(root->right);

    // Height of the given binary tree will be 1 greater than maximum of "leftHeight" and "rightHeight".
    int height = max(leftHeight, rightHeight) + 1;

    return height;
}

int getDiameter(TreeNode<int> *root)
{
    if (root == NULL)
    {
        // Diameter of an empty tree will be 0.
        return 0;
    }

    // Get the height of left and right subtrees.
    int leftHeight = getHeight(root->left);
    int rightHeight = getHeight(root->right);

    // Recur for left subtree and get the diameter.
    int leftDiameter = getDiameter(root->left);

    // Recur for right subtree and get the diameter.
    int rightDiameter = getDiameter(root->right);

    // Diameter of given binary tree.
    int diameter = max(leftDiameter, max(rightDiameter, leftHeight + rightHeight));

    return diameter;
}

int diameterOfBinaryTree(TreeNode<int> *root)
{
    return getDiameter(root);
}


```

# Approach - II
```cpp

/*
    Time Complexity : O(N)
    Space Complexity : O(N)
	
    Where 'N' is the number of nodes in the given binary tree.
*/

int getDiameter(TreeNode<int> *root, int &height)
{
    if (root == NULL)
    {
        // Height and diameter of an empty tree will be 0.
        height = 0;
        return 0;
    }

    // To store the height of left and right subtrees.
    int leftHeight = 0;
    int rightHeight = 0;

    // Recur for left subtree and get the height as well as diameter.
    int leftDiameter = getDiameter(root->left, leftHeight);

    // Recur for right subtree and get the height as well as diameter.
    int rightDiameter = getDiameter(root->right, rightHeight);

    // Update the height of the given binary tree.
    height = max(leftHeight, rightHeight) + 1;

    // Diameter of given binary tree.
    int diameter = max(leftDiameter, max(rightDiameter, leftHeight + rightHeight));

    return diameter;
}

int diameterOfBinaryTree(TreeNode<int> *root)
{
    // Initialize a variable to store the height of the of binary tree.
    int height = 0;

    // Recursive function to find diameter.
    return getDiameter(root, height);
}


```