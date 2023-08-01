# Find LCA of two nodes in BST


# Approach - I Depth - First Traversal
```cpp

/*
    Time Complexity: O(N)
    Space Complexity: O(N)

    where N is the total number of nodes of the BST.
*/


int findLCA(TreeNode<int>* currNode, TreeNode<int>* P, 
            TreeNode<int>* Q, TreeNode<int>* &LCA)
{
    if (currNode == NULL)
    {
        return 0;
    }

    int isTrueLeft = findLCA(currNode -> left, P, Q, LCA);
    int isTrueRight = findLCA(currNode -> right, P, Q, LCA);
    int isTrue = 0;

    if (currNode -> data == P -> data)
    {
        isTrue++;
    }

    if (currNode -> data == Q -> data)
    {
        isTrue++;
    }

    // Current Node is the LCA
    if (isTrueLeft + isTrueRight + isTrue >= 2)
    {
        LCA = currNode;
    }

    if (isTrueLeft + isTrueRight + isTrue)
    {
        return 1;
    }
    
    return 0;
}


TreeNode<int>* LCAinaBST(TreeNode<int>* root, TreeNode<int>* P, TreeNode<int>* Q)
{
    TreeNode<int>* LCA;

    findLCA(root, P, Q, LCA);

    return LCA;
}

```

# Approach - II Recursive Approach
```cpp

/*
    Time Complexity: O(N)
    Space Complexity: O(N)

    where N is the total number of nodes of the BST.
*/


TreeNode<int>* LCAinaBST(TreeNode<int>* root, TreeNode<int>* P, TreeNode<int>* Q)
{
	if (root -> data < P -> data && root -> data < Q -> data)
	{
		return LCAinaBST(root -> right, P, Q);
	}
	
	if (root -> data > P -> data && root -> data > Q -> data)
	{
		return LCAinaBST(root -> left, P, Q);
	}

	return root;
}

```

# Approach - III Iterative approach
```cpp

/*
    Time Complexity: O(N)
    Space Complexity: O(1)

    where N is the total number of nodes of the BST.
*/


TreeNode<int>* LCAinaBST(TreeNode<int>* root, TreeNode<int>* P, TreeNode<int>* Q)
{
	while (root != NULL)
	{
		if (root -> data < P -> data && root -> data < Q -> data)
		{
			root = root -> right;
		}
		else if (root -> data > P -> data && root -> data > Q -> data)
		{
			root = root -> left;
		}
		else
		{
			return root;
		}
	}
}

```