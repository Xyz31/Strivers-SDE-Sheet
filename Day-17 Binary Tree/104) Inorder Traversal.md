# Inorder Traversal

```md



```

# Approach - I
```cpp

/*
    Time Complexity: O( N )
    Space Complexity: O( N )

    where ‘N’ is the total number of nodes in the given binary tree.
*/

void inOrderHelper(TreeNode *node, vector<int> &answer)
{
    // Base case.
    if (node == NULL)
    {
        return;
    }

    // Visit left subtree.
    inOrderHelper(node->left, answer);

    // Add data of node to answer.
    answer.push_back(node->data);

    // Visit right subtree.
    inOrderHelper(node->right, answer);
}

vector<int> getInOrderTraversal(TreeNode *root)
{
    // Use answer to store traversal of nodes.
    vector<int> answer;

    // Call inOrderHelper function and store inOrder traversal in answer array.
    inOrderHelper(root, answer);

    // Return answer.
    return answer;
}

```

# Approach - II Morris
```cpp



vector < int > inorderTraversal(node * root) {
  vector < int > inorder;

  node * cur = root;
  while (cur != NULL) {
    if (cur -> left == NULL) {
      inorder.push_back(cur -> data);
      cur = cur -> right;
    } else {
      node * prev = cur -> left;
      while (prev -> right != NULL && prev -> right != cur) {
        prev = prev -> right;
      }

      if (prev -> right == NULL) {
        prev -> right = cur;
        cur = cur -> left;
      } else {
        prev -> right = NULL;
        inorder.push_back(cur -> data);
        cur = cur -> right;
      }
    }
  }
  return inorder;
}

```