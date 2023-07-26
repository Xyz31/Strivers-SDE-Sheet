# Root to Node Path in Binary Tree

# Approach - I
```cpp

#include <bits/stdc++.h> 
/*   
    template <typename T = int>
	class TreeNode
	{
		public:
		T data;
		TreeNode<T> *left;
		TreeNode<T> *right;

		TreeNode(T data)
		{
			this->data = data;
			left = NULL;
			right = NULL;
		}

		~TreeNode()
		{
			if (left != NULL)
			{
		  		delete left;
			}
			if (right != NULL)
			{
			 	delete right;
			}
		}
	};
*/

// Depth-first search to find the path from the root node to the target node
// Returns true if the target node is found, false otherwise
// Time complexity: O(n), where n is the number of nodes in the binary tree
// Space complexity: O(h), where h is the height of the binary tree
bool dfs(TreeNode<int> *node, int x, vector<int> &path) {
    if (node == nullptr) {
        return false;
    }
    
    // Add the current node to the path
    path.push_back(node->data);
    
    // Check if the current node is the target node
    if (node->data == x) {
        return true;
    }
    
    // Recursively search in the left and right subtrees
    if (dfs(node->left, x, path) || dfs(node->right, x, path)) {
        return true;
    }
    
    // If the target node is not found in the subtree, remove the current node from the path
    path.pop_back();
    
    return false;
}

// Finds the path from the root node to the given target node in a binary tree
// Returns the path as a vector of integers
// Time complexity: O(n), where n is the number of nodes in the binary tree
// Space complexity: O(h), where h is the height of the binary tree
vector<int> pathInATree(TreeNode<int> *root, int x) {
    vector<int> path;
    
    dfs(root, x, path);
    
    return path;
}




```

# Approach - II
```cpp



```