# LeftView Of Binary Tree

# Approach - I
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

void leftView(vector<int>&res, TreeNode<int>* root, int level)
{
    if(root == NULL) return;

    if(level == res.size()) res.push_back(root->data);

    leftView(res, root->left, level + 1);
    leftView(res, root->right, level + 1);
}



vector<int> getLeftView(TreeNode<int> *root)
{
    //    Write your code here
    vector<int> res;
    leftView(res,root,0);
    return res;
}

```

# Approach - II
```cpp



```