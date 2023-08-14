# Maximum path sum


```md



```

# Approach - I
```cpp

/*  
    Time Complexity : O(N^2)
    Space Complexity : O(N)
    
    where 'N' is the number of nodes in the Binary Tree.
*/

#include <algorithm>

// Function to calculate the maximum sum from node to leaf.
long long int findMaxSumNodeToLeaf(TreeNode<int> *root)
{
    if (root == NULL)
    {
        return 0;
    }

    long long int maxSumLeftPath = findMaxSumNodeToLeaf(root->left);
    long long int maxSumRightPath = findMaxSumNodeToLeaf(root->right);

    long long int maxSumFromNodeToLeaf = root->val + max(maxSumLeftPath, maxSumRightPath);

    return maxSumFromNodeToLeaf;
}

// Function to calculate the maximum sum of path between two leaves that passes through a node.
long long int findMaxSumPathViaNode(TreeNode<int> *root)
{
    if (root == NULL)
    {
        return -1;
    }

    // Variable to store the maximum sum of path between two leaves for the given tree.
    long long int maxPathSum = -1;

    // Variable to store the max length of path from left child to leaf.
    long long int maxSumPathFromLeft = findMaxSumNodeToLeaf(root->left);
    // Variable to store the max length of path from right child to leaf.
    long long int maxSumPathFromRight = findMaxSumNodeToLeaf(root->right);

    if (root->left != NULL && root->right != NULL)
    {
        long long int maxSumPathViaNode = maxSumPathFromLeft + maxSumPathFromRight + root->val;
        maxPathSum = max(maxPathSum, maxSumPathViaNode);
    }

    maxPathSum = max({maxPathSum, findMaxSumPathViaNode(root->left), findMaxSumPathViaNode(root->right)});

    return maxPathSum;
}

long long int findMaxSumPath(TreeNode<int> *root)
{
    return findMaxSumPathViaNode(root);
}

```

# Approach - II
```cpp

#include <bits/stdc++.h> 
/************************************************************

    Following is the Tree node structure
	
	template <typename T>
    class TreeNode 
    {
        public : 
        T val;
        TreeNode<T> *left;
        TreeNode<T> *right;

        TreeNode(T val) 
        {
            this -> val = val;
            left = NULL;
            right = NULL;
        }
    };

************************************************************/

/*

Time Complexity: The time complexity of the maxPath function is O(n), where n is the number of nodes in the binary tree. 
This is because we visit each node exactly once in a depth-first manner. The findMaxSumPath function has the same time complexity as maxPath.
Space Complexity: The space complexity of the code is O(h), where h is the height of the binary tree. 
This is because the space required by the call stack during the recursive calls is proportional to the height of the tree.

*/

#define ll long long

// Function to find the maximum sum path in a binary tree
int maxPath(TreeNode<int>* node, ll &mx)
{
    // Base case: if the node is NULL, return 0
    if (node == NULL) return 0;
    
    // Recursively calculate the maximum path sum in the left subtree
    ll left = max(0, maxPath(node->left, mx));
    
    // Recursively calculate the maximum path sum in the right subtree
    ll right = max(0, maxPath(node->right, mx));
    
    // Update the maximum path sum if the current path sum (left + right + node->val) is greater
    mx = max(mx, left + right + node->val);
    
    // Return the maximum path sum from the current node to its parent
    return max(left, right) + node->val;
}

// Function to find the maximum sum path in a binary tree
long long int findMaxSumPath(TreeNode<int>* root)
{
    // If the root is NULL or it has only one child (leaf node), return -1
    if (!root || !root->left || !root->right) return -1;
    
    // Initialize the maximum sum as the minimum possible value
    ll mx = INT_MIN;
    
    // Call the helper function to find the maximum sum path
    maxPath(root, mx);
    
    // Return the maximum sum path
    return mx;
}


```