# Construct A Binary Tree from Inorder and Postorder Traversal


# Approach - I
```cpp

/************************************************************
   
   Following is the TreeNode class structure
   
   class TreeNode<T>
   { 
   public:
        T data; 
        TreeNode<T> *left;
        TreeNode<T> *right;
   
        TreeNode(T data) 
  		{ 
            this -> data = data; 
            left = NULL; 
            right = NULL; 
        }
   };
   
   
 ************************************************************/
/*

the total time complexity to construct the binary tree is O(n), where n is the number of elements in the inorder traversal. 
the space complexity is O(n) due to the recursive stack space and the auxiliary vectors.
*/



// Helper function to build the tree recursively
TreeNode<int> *build_helper(vector<int> &postorder, vector<int> &inorder, int start, int end, int &post_index) {
    // Base case: if the start index exceeds the end index, there are no elements to process
    if (start > end) {
        return NULL;
    }

    // Create a new tree node using the value from the postorder traversal at the current post_index
    TreeNode<int> *root = new TreeNode<int>(postorder[post_index]);

    // Find the index of the current root value in the inorder traversal
    int idx = -1;
    for (int i = start; i <= end; i++) {
        if (inorder[i] == postorder[post_index]) {
            idx = i;
            break;
        }
    }

    // Decrease the post_index to move to the next element in the postorder traversal
    post_index--;

    // Recursive calls to build the right and left subtrees
    // The right subtree elements come before the current root in the inorder traversal, so the range is [idx + 1, end]
    root->right = build_helper(postorder, inorder, idx + 1, end, post_index);
    // The left subtree elements come after the current root in the inorder traversal, so the range is [start, idx - 1]
    root->left = build_helper(postorder, inorder, start, idx - 1, post_index);

    return root;
}

// Main function to construct the tree using postorder and inorder traversals
TreeNode<int>* getTreeFromPostorderAndInorder(vector<int>& postOrder, vector<int>& inOrder) {
    int n = postOrder.size();
    int post_index = n - 1; // Start with the last element of the postorder traversal

    // Call the helper function to build the tree
    return build_helper(postOrder, inOrder, 0, n - 1, post_index);
}



```

