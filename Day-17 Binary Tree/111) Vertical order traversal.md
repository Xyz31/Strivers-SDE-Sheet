# Vertical order traversal

# Approach - I
```cpp

#include <bits/stdc++.h> 
/************************************************************

Following is the Binary Tree node class
    
template <typename T = int>
class TreeNode
{
public:
    T data;
    TreeNode<T> *left;
    TreeNode<T> *right;

    TreeNode(T val)
    {
        this->data = val;
        left = NULL;
        right = NULL;
    }

    ~TreeNode()
    {
        if (left != NULL)
        {
            delete left;
        }
        if (right != NULL)
        {
            delete right;
        }
    }
};

************************************************************/
/*

Complexities:

Time Complexity: The time complexity of the algorithm is O(n log n), where n is the number of nodes in the binary tree. 
This is because we are performing a level-order traversal of the tree, which takes O(n) time, and for each node, we are inserting it into the verticalMap, which takes O(log n) time on average due to the use of a balanced binary search tree (map). 
Therefore, the overall time complexity is O(n log n).
Space Complexity: The space complexity of the algorithm is O(n), where n is the number of nodes in the binary tree. 
This is because we are using additional space to store the nodes in the verticalMap and the queues for level-order traversal. 
In the worst case, the verticalMap can contain all the nodes of the tree, which contributes to the space complexity.

*/

vector<int> verticalOrderTraversal(TreeNode<int> *root)
{
    //    Write your code here.
    vector<int> result;
    
    if (root == nullptr) {
        return result;
    }
    
    // Map to store nodes based on their vertical positions
    map<int, vector<int>> verticalMap;
    
    // Queue for level-order traversal
    queue<pair<TreeNode<int>*, int>> nodeQueue;
    
    // Queue to keep track of the horizontal positions of the nodes
    queue<int> positionQueue;
    
    nodeQueue.push({root, 0});
    positionQueue.push(0);
    
    while (!nodeQueue.empty()) {
        TreeNode<int> *node = nodeQueue.front().first;
        int pos = nodeQueue.front().second;
        nodeQueue.pop();
        
        int horPos = positionQueue.front();
        positionQueue.pop();
        
        verticalMap[horPos].push_back(node->data);
        
        if (node->left) {
            nodeQueue.push({node->left, pos + 1});
            positionQueue.push(horPos - 1);
        }
        
        if (node->right) {
            nodeQueue.push({node->right, pos + 1});
            positionQueue.push(horPos + 1);
        }
    }
    
    for (auto it = verticalMap.begin(); it != verticalMap.end(); ++it) {
        vector<int> values = it->second;
        for (int i = 0; i < values.size(); ++i) {
            result.push_back(values[i]);
        }
    }
    
    return result;
}


```

# Approach - II
```cpp



```