# Binary Tree to Double Linked List


```md



```
 
# Approach - I 
```cpp

/*
    Time Complexity - O(N^2)
    Space Complexity - O(N)

    where 'N' is the number of nodes in the tree.
*/

/*************************************************************
 
        Following is the Binary Tree node structure

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

*************************************************************/

BinaryTreeNode<int>* BTtoDLL(BinaryTreeNode<int>* root) {

    // Base case.
    if(root == NULL)
    {
        return root;
    }

    if(root->left != NULL)
    {
        BinaryTreeNode<int>* left = BTtoDLL(root->left);

        // Inorder predecessor.
        while(left->right != NULL)
        {
            left = left->right;
        }

        left->right = root;
        root->left = left;
    }

    if(root->right != NULL)
    {
        BinaryTreeNode<int>* right = BTtoDLL(root->right);

        // Inorder successor.
        while(right->left != NULL)
        {
            right = right->left;
        }

        right->left = root;
        root->right = right;
    }

    while (root->left != NULL)
    {
        root = root->left;
    }

    return root;
}

```

# Approach - II Recursive Solution - 2
```cpp

/*
    Time Complexity - O(N)
    Space Complexity - O(N)

    where 'N' is the number of nodes in the tree.
*/

/*************************************************************
 
        Following is the Binary Tree node structure

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

*************************************************************/

void findHead(BinaryTreeNode<int> *root, BinaryTreeNode<int> **head, BinaryTreeNode<int> **prev) {
    
    // Base case.
    if(root == NULL)
    {
        return ;
    }

    findHead(root->left, head, prev);

    if(*prev == NULL)
    {
        *head = root;
    }
    else
    {
        root->left = *prev;
        (*prev)->right = root;
    }

    *prev = root;

    findHead(root->right, head, prev);
}

BinaryTreeNode<int>* BTtoDLL(BinaryTreeNode<int>* root) {
    BinaryTreeNode<int>* head = NULL;
    BinaryTreeNode<int>* prev = NULL;
    findHead(root, &head, &prev);

    return head;
}

```