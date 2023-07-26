# Preorder Traversal

# Approach - I
```cpp

#include <bits/stdc++.h> 
/*
    Following is Binary Tree Node structure:
    class TreeNode
    {
    public:
        int data;
        TreeNode *left, *right;
        TreeNode() : data(0), left(NULL), right(NULL) {}
        TreeNode(int x) : data(x), left(NULL), right(NULL) {}
        TreeNode(int x, TreeNode *left, TreeNode *right) : data(x), left(left), right(right) {}
    };
*/


void preorder(TreeNode* root, vector<int>& nodes) {
        if (!root) return;

        nodes.push_back(root -> data);
        preorder(root -> left, nodes);
        preorder(root -> right, nodes);
    }

vector<int> getPreOrderTraversal(TreeNode *root)
{
    // Write your code here.
    vector<int> nodes;
        preorder(root, nodes);
        return nodes;
    
}

```

# Approach - II Morris Traversal
```cpp


vector < int > preorderTraversal(node * root) {
  vector < int > preorder;

  node * cur = root;
  while (cur != NULL) {
    if (cur -> left == NULL) {
      preorder.push_back(cur -> data);
      cur = cur -> right;
    } else {
      node * prev = cur -> left;
      while (prev -> right != NULL && prev -> right != cur) {
        prev = prev -> right;
      }

      if (prev -> right == NULL) {
        prev -> right = cur;
        preorder.push_back(cur -> data);
        cur = cur -> left;
      } else {
        prev -> right = NULL;
        cur = cur -> right;
      }
    }
  }
  return preorder;
}


```