# Size of the largest BST in a Binary Tree

```md



```
 

# Approach - I Brute Force
```cpp

/*
    Time Complexity: O(N^2)
    Space Complexity: O(N)
    
    where 'N' is the total number of nodes in the binary tree.
*/

bool isBST(TreeNode<int>* root, int min, int max)
{
	if (root == NULL)
	{
		return true;
	}

	if (root -> data < min || root -> data > max)
	{
		return false;
	}

	return isBST(root -> left, min, root -> data - 1) && 
		   isBST(root -> right, root -> data + 1, max);
}


int size(TreeNode<int>* root)
{
	if (root == NULL)
	{
		return 0;
	}
	
	return 1 + size(root -> left) + size(root -> right);
}


int largestBST(TreeNode<int>* root)
{
	// Current Subtree is BST.
	if (isBST(root, INT_MIN, INT_MAX) == true)
	{
		return size(root);
	}
	
	// Find largest BST in left and right subtrees.
	return max(largestBST(root -> left), largestBST(root -> right));
}

```

# Approach - II Bottom-up Traversal of BST
```cpp

/*
    Time Complexity: O(N)
    Space Complexity: O(N)
    
    where 'N' is the total number of nodes in the binary tree.
*/

struct info 
{
	bool isValid;
	int size, min, max;
};

info maxSize(TreeNode<int>* currNode, int &maxBST)
{
	if (currNode == NULL)
	{
		// isValid, size, min, max.
		return {true, 0, INT_MAX, INT_MIN};
	}


	// Information of left and right subtrees.
	info left = maxSize(currNode -> left, maxBST);
	info right = maxSize(currNode -> right, maxBST);


	info currInfo;

	// Size of current subtree.
	currInfo.size = left.size + right.size + 1;
	
	// Left and Right subtrees must be BST.
	currInfo.isValid = left.isValid & right.isValid;
	
	// Current subtree must form a BST.
	currInfo.isValid &= (currNode -> data > left.max);
	currInfo.isValid &= (currNode -> data < right.min);
	
	// Updating min and max for current subtree.
	currInfo.min = min(min(left.min, right.min), currNode -> data);
	currInfo.max = max(max(left.max, right.max), currNode -> data);


	if (currInfo.isValid == true)
	{
		maxBST = max(maxBST, currInfo.size);
	}

	return currInfo;
}


int largestBST(TreeNode<int>* root)
{
	int maxBST = 0;

	maxSize(root, maxBST);

	return maxBST;
}

```