# Construct a BST from a preorder traversal


```md



```

# Approach - I Recursive Approach
```cpp

/*
    Time Complexity: O(N^2)
    Space Complexity: O(N^2)

    Where N is the number nodes in the tree.
*/

// Utility function to get the the tree from preOrder traversal
TreeNode<int>* util(vector<int> &preOrder){

    // If the length of the preOrder traversal is 0 return NULL.
    if(preOrder.size() == 0){
        return NULL;
    }

    // Set the root as the first element of the preOrder traversal.
    TreeNode<int>* root = new TreeNode<int>(preOrder[0]);

    // All the nodes smaller than the root will go in the left subtree.
    vector<int> leftPreOrder;
    for(int i = 1; i < preOrder.size(); i++){
        if(preOrder[i] < preOrder[0]){
            leftPreOrder.push_back(preOrder[i]);
        }
    }

    // All the nodes greater than the root will go in the right subtree.
    vector<int> rightPreOrder;
    for(int i = 1; i < preOrder.size(); i++){
        if(preOrder[i] > preOrder[0]){
            rightPreOrder.push_back(preOrder[i]);
        }
    }

    // Call the util function on left and right subtree of the root.
    root -> left = util(leftPreOrder);
    root -> right = util(rightPreOrder);

    // Return the root.
    return root;
}


TreeNode<int>* preOrderTree(vector<int> &preOrder){

    // Return the util function.
    return util(preOrder);
}

```

# Approach - II optimised approach
```cpp

/*
    Time Complexity: O(N)
    Space Complexity: O(N)

    Where N is the number of nodes in the tree.
*/

#include<climits>

TreeNode<int>* util(vector<int> &preOrder, int &preIndex, int startRange, int endRange){

    // If the preIndex is greater than the length of the array return NULL.
    if (preIndex >= preOrder.size()){
        return NULL;
    }

    int currNode = preOrder[preIndex];

    // If the current node lies inside the range then process the node.
    if (currNode > startRange && currNode < endRange){
        TreeNode<int>* root = new TreeNode<int>(currNode);

        // Increase the index by 1.
        preIndex += 1;

        // If left node exists process left.
        if (preIndex < preOrder.size()){
            root -> left = util(preOrder, preIndex, startRange, currNode);
        }
        // If right node exists process right.
        if (preIndex < preOrder.size()){
            root -> right = util(preOrder, preIndex, currNode , endRange);
        }

        // Return the root.
        return root;
    }

    // If node was not processed return NULL.
    return NULL;
}

TreeNode<int>* preOrderTree(vector<int> &preOrder){
    
    int preIndex = 0;

    // Return the util function.
    return util(preOrder, preIndex, INT_MIN, INT_MAX);
}

```