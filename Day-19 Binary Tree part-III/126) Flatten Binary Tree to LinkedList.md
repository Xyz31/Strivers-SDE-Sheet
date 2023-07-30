# Flatten Binary Tree to LinkedList


# Approach - I
```cpp

/*
    Time Complexity - O(N)
    Space Complexity - O(N)

    Where N is the number of nodes in the Binary Tree.
*/

void preOrderTraversal(TreeNode<int> *root, vector<int> &preOrder)
{
    if (root == NULL)
        return;

    preOrder.push_back(root->data);

    preOrderTraversal(root->left, preOrder);
    preOrderTraversal(root->right, preOrder);
}

TreeNode<int> *flattenBinaryTree(TreeNode<int> *root)
{
    vector<int> preOrder;

    // Find the pre-order traversal of the tree and store it in a list.
    preOrderTraversal(root, preOrder);

    // Create a new linked list from the stored values.
    TreeNode<int> *head = root;

    for (int i = 1; i < preOrder.size(); i++)
    {
        root->right = new TreeNode<int>(preOrder[i]);

        root = root->right;
    }

    return head;
}


```

# Approach - II
```cpp

/*
    Time Complexity - O(N)
    Space Complexity - O(N)

    Where N is the number of nodes in the Binary Tree.
*/

#include <stack>

TreeNode<int> *flattenBinaryTree(TreeNode<int> *root)
{
    stack<TreeNode<int> *> stk;

    TreeNode<int> *head = root;

    while (root != NULL || !stk.empty())
    {
        if (root->right != NULL)
        {
            stk.push(root->right);
        }

        if (root->left != NULL)
        {
            // Make the left child as the new right child of the node.
            root->right = root->left;
            root->left = NULL;
        }
        else if (!stk.empty())
        {
            // Pop the top node from the stack.
            // Make it the right child of the current node.
            root->right = stk.top();
            stk.pop();
        }

        // Set the right child of the node as the current node.
        root = root->right;
    }

    return head;
}


```
# Approach - III
```cpp

/*
    Time Complexity - O(N)
    Space Complexity - O(N)

    Where N is the number of nodes in the Binary Tree.
*/

TreeNode<int> *flattenBinaryTreeHelper(TreeNode<int> *currentNode, TreeNode<int> *lastNode)
{
    if (currentNode == NULL)
    {
        // Base Condition.
        return lastNode;
    }

    if (lastNode != NULL)
    {
        // Set currentNode as the right child of the lastNode.
        lastNode->right = currentNode;
    }

    // Store the left and right child of the currentNode in temporary variables.
    TreeNode<int> *left = currentNode->left;
    TreeNode<int> *right = currentNode->right;

    // Set the left and right pointers of currentNode to NULL.
    currentNode->left = currentNode->right = NULL;

    TreeNode<int> *newLastNode = flattenBinaryTreeHelper(left, currentNode);

    newLastNode = flattenBinaryTreeHelper(right, newLastNode);

    return newLastNode;
}

TreeNode<int> *flattenBinaryTree(TreeNode<int> *root)
{
    TreeNode<int> *head = root;

    flattenBinaryTreeHelper(root, NULL);

    return head;
}


```