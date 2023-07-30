# LCA in Binary Tree


# Approach - I
```cpp

/*
    Time Complexity : O(N)
    Space Complexity : O(N)

    Where 'N' is the number of nodes in the given binary tree.
*/

//    Finds the path from root to 'X' and return true if it exists.
bool getPath(TreeNode<int> *root, vector<int> &path, int x)
{

	if (root == NULL)
	{
		//    Tree doesn't have any node.
		return false;
	}

	//    Store the root node in the path
	path.push_back(root->data);

	//    Check if we reached to the destination node i.e. 'X'
	if (root->data == x)
	{
		//    'X' is found.
		return true;
	}

	//    Recur to find 'X' in the left subtree.
	if (getPath(root->left, path, x))
	{
		//    'X' exists in the left subtree.
		return true;
	}

	//    Recur to find 'X' in the right subtree.
	if (getPath(root->right, path, x))
	{
		//    'X' exists in the right subtree.
		return true;
	}

	//    Remove the root node because 'X' doesn't exists in the subtree rooted at "root".
	path.pop_back();

	return false;
}

int lowestCommonAncestor(TreeNode<int> *root, int x, int y)
{
	//    To store the path from the root node to 'X' and 'Y'
	vector<int> pathToX, pathToY;

	//    Get the path from the root node to node 'X'
	getPath(root, pathToX, x);

	//    Get the path from the root node to node 'Y'
	getPath(root, pathToY, y);

	int index;

	//    Iterate while elements in the lists are equal.
	for (index = 0; index < min(pathToX.size(), pathToY.size()); index++)
	{
		if (pathToX[index] != pathToY[index])
		{
			//    Elements are not same.
			break;
		}
	}

	//    Return the LCA.
	return pathToX[index - 1];
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


/*
int lowestCommonAncestor(TreeNode<int> *root, int x, int y)
{
	//    Write your code here
}
*/

/*
    Time Complexity : O(N)
    Space Complexity : O(N)
	
    Where 'N' is the number of nodes in the given binary tree.
*/
int lowestCommonAncestor(TreeNode<int>* root, int x, int y) {
    // If the root is null, return -1 indicating that the tree is empty
    if (root == nullptr) {
        return -1;
    }

    // If the root's data matches either x or y, it is the lowest common ancestor
    if (root->data == x || root->data == y) {
        return root->data;
    }

    // Recursively find the lowest common ancestor in the left and right subtrees
    int left = lowestCommonAncestor(root->left, x, y);
    int right = lowestCommonAncestor(root->right, x, y);

    // If both left and right subtrees return valid values (not -1), then the current root is the lowest common ancestor
    if (left != -1 && right != -1) {
        return root->data;
    }

    // If only the left subtree returns a valid value, return it as the lowest common ancestor
    if (left != -1) {
        return left;
    }

    // If only the right subtree returns a valid value, return it as the lowest common ancestor
    return right;
}


```