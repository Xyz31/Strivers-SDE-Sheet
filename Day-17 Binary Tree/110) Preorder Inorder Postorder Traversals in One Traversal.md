# Preorder Inorder Postorder Traversals in One Traversal

# Approach - I
```cpp

#include <bits/stdc++.h> 
/************************************************************

    Following is the Binary Tree node structure:

    class BinaryTreeNode
    {
    public :
        T data;
        BinaryTreeNode<T> *left;
        BinaryTreeNode<T> *right;

        BinaryTreeNode(T data) {
            this -> data = data;
            left = NULL;
            right = NULL;
        }
    };


************************************************************/
/*
The time complexity of the function is O(n), where n is the number of nodes in the tree.
*/
vector<vector<int>> getTreeTraversal(BinaryTreeNode<int> *root){
    // Write your code here.
    vector<vector<int>> result(3, vector<int>());
    if (root == NULL)
        return result;

    stack<pair<BinaryTreeNode<int>*, int>> st;
    st.push({ root, 0 });

    while (!st.empty()) {
        auto x = st.top();
        st.pop();

        if (x.second == 0) {
            result[1].push_back({ x.first->data });
            x.second++;
            st.push(x);
            if (x.first->left != NULL) {
                st.push({ x.first->left, 0 });
            }
        } else if (x.second == 1) {
            result[0].push_back({ x.first->data });
            x.second++;
            st.push(x);
            if (x.first->right != NULL) {
                st.push({ x.first->right, 0 });
            }
        } else {
            result[2].push_back({ x.first->data });
        }
    }
}

```

# Approach - II
```cpp



```