# Find K-th largest element in BST

```md



```
 

# Approach - I
```cpp

/*
    Time Complexity: O(N)
    Space Complexity: O(N)

    where 'N' is the total number of nodes of the BST.
*/

void inorder(TreeNode<int>* root, vector<int>& inTraversal)
{
	if (root == NULL)
	{
		return;
	}

	// Recurse over left subtree. 
	inorder(root -> left, inTraversal);

    inTraversal.push_back(root -> data);

	// Recurse over right subtree.
	inorder(root -> right, inTraversal);
}


int KthLargestNumber(TreeNode<int>* root, int k)
{
	vector <int> inTraversal;

	inorder(root, inTraversal);

	int n = inTraversal.size();

	if (k > n)
	{
		return -1;
	}
	
	return inTraversal[n - k];
}

```

# Approach - II Reverse Inorder Traversal
```cpp

/*
    Time Complexity: O(N)
    Space Complexity: O(N)

    where 'N' is the total number of nodes of the BST.
*/

int revInorder(TreeNode<int>* root, int &visCount, int k)
{
	if (root == NULL)
	{
		return -1;
	}
	
	// Recurse over right subtree. 
	int right = revInorder(root -> right, visCount, k);
    
    if (right != -1)
    {
    	return right;
    }

	visCount++;

	if (visCount == k)
	{
		return root -> data;
	}

	// Recurse over left subtree.
	int left = revInorder(root -> left, visCount, k);
    
    return left;
}


int KthLargestNumber(TreeNode<int>* root, int k)
{
	int visCount = 0;

	return revInorder(root, visCount, k);
}

```