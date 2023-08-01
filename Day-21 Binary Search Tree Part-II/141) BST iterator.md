# BST iterator


# Approach - I Tree flattening
```cpp

/*
	Time Complexity: O(N)
	Space complexity: O(N)

	Where 'N' is the number of nodes.

*/

class BSTiterator
{
public:
	
	// Create a list to store node's value in sorted order
	vector<int> nodeValues;
	
	// This will be used to iterate over the list
	int index;

	BSTiterator(TreeNode<int> *root)
	{
		index = 0;
		inorder(root);
	}

	int next()
	{
		int nextSmallest = nodeValues[index];
	
		// Increment the index for next smallest element
		++index;
		return nextSmallest;
	}

	bool hasNext()
	{
	
		// If index is less than size of the list that means there are still some nodes left for processing
		if (index < nodeValues.size())
		{
			return true;
		}
		else
		{
			return false;
		}
	}

	// This function will used to perform inorder traversal on the BST
	void inorder(TreeNode<int> *root)
	{
		if (root == NULL)
		{
			return;
		}
	
		// Traverse on the left child
		inorder(root->left);
	
		// Store the data
		nodeValues.push_back(root->data);
	
		// Traverse on the right child
		inorder(root->right);
	}
};

```

# Approach - II Stack
```cpp

/*
	Time Complexity: O(N)
	Space complexity: O(N)

	Where 'N' is the number of nodes.

*/

#include <stack>

class BSTiterator
{
public:
	
    // Create a stack which will store smallest element at the top
    stack<TreeNode<int> *> st;

    BSTiterator(TreeNode<int> *root)
    {
    	
        // Fill the stack with leftmost nodes present in the subtree of root
        leftMostInorder(root);
    }

    int next()
    {
    	
        // Pop the minimum
        TreeNode<int> *top = st.top();
        st.pop();
        
        // Check if it has right child
        if (top->right != NULL)
        {
        
            // Push leftmost nodes present in the subtree of right child
            leftMostInorder(top->right);
        }
        return top->data;
    }

    bool hasNext()
    {
        
        // If size of stack is greater than zero that means there are still some nodes left for processing
        if (st.size() > 0)
        {
            return true;
        }
        else
        {
            return false;
        }
    }

    // This function will used to push leftmost nodes in the stack present in the subtree of root
    void leftMostInorder(TreeNode<int> *root)
    {
        while (root != NULL)
        {
            st.push(root);
            root = root->left;
        }
    }
};

```