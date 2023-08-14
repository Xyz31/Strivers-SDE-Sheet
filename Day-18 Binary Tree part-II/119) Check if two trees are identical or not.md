# Check if two trees are identical or not

```md



```

# Approach - I
```cpp

/*
    Time complexity: O( max(M, N) ) 
    Space complexity: O( max(M, N) )
    
    M and N are number of nodes in binary tree 1 and binary tree 2 respectively.
*/

#include<queue>

vector<int> createLevelOrder(BinaryTreeNode<int>*root) {
    
    // Res will store level order traversal of the tree. 
    vector<int> res;
    
    if(root == NULL) {
        res.push_back(-1);
        return res;
    }
    
    // Using queue to implement level order traversal. 
    queue<BinaryTreeNode<int>*> q;
    
    q.push(root);
    res.push_back(root->data);
    
    while(!q.empty()) {
        
        BinaryTreeNode<int>* first = q.front();
        
        // Push the left child into queue   
        if(first->left != NULL) {
            q.push(first->left);
            res.push_back(first->left->data);
        }
        else {
            // Push -1 for NULL node. 
            res.push_back(-1);
        }
        
        // Push the right child into queue  
        if(first->right != NULL) {
            q.push(first->right);
            res.push_back(first->right->data);
        }
        else {
            // Push -1 for NULL node. 
            res.push_back(-1);
        }
        
        // Pop out the explored Node.   
        q.pop(); 

    }
    
    return res;

}


bool identicalTrees(BinaryTreeNode<int>* root1, BinaryTreeNode<int>* root2) {
    
    // Store level order of tree 1 in arr1.      
    vector<int> arr1 = createLevelOrder(root1);
    
    // Store level order of tree 2 in arr2. 
    vector<int> arr2 = createLevelOrder(root2);
    
    if(arr1.size() != arr2.size()) {
        return false;
    }
    
    // Check if level order is same or not. 
    for(int i = 0; i < arr1.size(); i++) {
        if(arr1[i] != arr2[i]) {
            return false;
        }
    }
    
    return true;
    
}



```

# Approach - II
```cpp

#include <bits/stdc++.h> 
/**********************************************************

    Following is the Binary Tree Node class structure:

    template <typename T>

    class BinaryTreeNode {
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

***********************************************************/
/**
 * This function checks if two binary trees are identical or not.
 * The return type of the function is `bool`.
 * The function takes two pointers to the roots of the binary trees, `p` and `q`, as input.
 * It recursively compares the nodes of the two trees to determine if they are identical.
 * If both trees are NULL, they are considered identical and the function returns true.
 * If one tree is NULL and the other is not, they are not identical and the function returns false.
 * If the data of the current nodes in the trees is different, they are not identical and the function returns false.
 * Otherwise, the function recursively checks the left and right subtrees of the nodes.
 * The function returns the logical AND of the recursive calls for the left and right subtrees.
 * The time complexity of the function is O(n), where n is the number of nodes in the smaller tree.
 */

/*
    Time complexity: O(min(M, N)) 
    Space complexity: O(min(H1, H2)
    
    M and N are number of nodes and H1 and H2 are heights of binary tree 1 and binary tree 2 respectively.
*/
bool identicalTrees(BinaryTreeNode<int>* p, BinaryTreeNode<int>* q) {
    if (p == NULL && q == NULL)
        return true;

    if (p == NULL || q == NULL)
        return false;

    if (p->data != q->data)
        return false;

    return identicalTrees(p->left, q->left) && identicalTrees(p->right, q->right);
}


```