# Find K-th smallest element in BST


# Approach - I Recursive Inorder Traversal
```cpp

/*
    Time Complexity : O(N)
    Space Complexity : O(N)

    Where 'N' is the number of nodes in the given binary search tree.
*/

//	Stores the inorder traversal of the tree in "nodes".
void inorder(TreeNode<int> *root, vector<int> &nodes)
{
	if (root == NULL)
	{
		//	Base case.
		return;
	}

	//	Recur for the left subtree.
	inorder(root->left, nodes);

	//	Store the current node value in "nodes".
	nodes.push_back(root->data);

	//	Recur for the right subtree.
	inorder(root->right, nodes);
}

int kthSmallest(TreeNode<int> *root, int k)
{
	//	To store the inorder traversal of the BST.
	vector<int> nodes;

	inorder(root, nodes);

	return nodes[k - 1];
}

```

# Approach - II Iterative Inorder Traversal
```cpp

/*
    Time Complexity : O(N)
    Space Complexity : O(N)

    Where 'N' is the number of nodes in the given binary search tree.
*/

#include <stack>

int kthSmallest(TreeNode<int> *root, int k)
{
	//	To store the nodes of the tree.
	stack<TreeNode<int> *> st;

	while (1)
	{
		while (root != NULL)
		{
			//	Push the root node in the stack.
			st.push(root);

			root = root->left;
		}

		root = st.top();
		st.pop();

		if (k == 1)
		{
			return root->data;
		}

		//	Update the 'k'
		k = k - 1;

		root = root->right;
	}
}

```