# Zig Zag Traversal of Binary Tree


```md



```

# Approach - I
```cpp

/*
    Time Complexity  : O(N^2)
    Space Complexity : O(N)

    where N is the number of nodes in the binary tree
*/

#include <vector>

// Function to get maximum level of binary tree
int getMaxLevel(BinaryTreeNode<int>* curNode)
{
    // If curNode is NULL means depth of its subtree will be zero.
    if (curNode == NULL)
    {
        return 0;
    }

    // Find maximum depth of right subtree
    int leftSubtreeDepth = getMaxLevel(curNode -> left);

    // Find maximum depth of right subtree
    int rightSubtreeDepth = getMaxLevel(curNode -> right);

    // maximum level will be 1 + maximum of depth between left and right subtree
    return 1 + max(leftSubtreeDepth, rightSubtreeDepth);
}

/* Function to traverse a given level of a binary tree
  If direction is 0, we traverse left to right
  If direction is 1, we traverse right to left
*/
void traverseLevel(BinaryTreeNode<int>* curNode, vector<int>& answer, int curLevel, int targetLevel, int direction)
{
    // If cur node is NULL then return
    if (curNode == NULL)
    {
        return;
    }

    // If curLevel equals to target level then add data of node to answer
    if (curLevel == targetLevel)
    {
        answer.push_back(curNode -> data);
        return;
    }

    //  If direction is 0, we first go from left to right
    if (direction == 0)
    {
        traverseLevel(curNode -> left, answer, curLevel + 1, targetLevel, direction);
        traverseLevel(curNode -> right, answer, curLevel + 1, targetLevel, direction);
    }
    //  If direction is 1, we first go from right to left
    else
    {
        traverseLevel(curNode -> right, answer, curLevel + 1, targetLevel, direction);
        traverseLevel(curNode -> left, answer, curLevel + 1, targetLevel, direction);
    }
}

vector<int> zigZagTraversal(BinaryTreeNode<int>* root)
{
    // Declare array to store the zigzag traversal of the binary tree
    vector<int> answer;

    // Find the curLevel of the tree
    int maxLevel = getMaxLevel(root);

    //   Variable to keep track of traversing direction
    bool direction = 0;

    // Traverse each level in the tree
    for (int level = 1; level <= maxLevel; level++)
    {
        // Traverse the current level
        traverseLevel(root, answer, 1, level, direction);

        // Toggle the direction variable
        direction ^= 1;
    }

    // Return answer order
    return answer;
}

```

# Approach - II
```cpp

#include <bits/stdc++.h> 
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

/*
The time complexity of the code is O(N),

*/
// This function performs a zigzag traversal of a binary tree and returns the result as a vector of integers.
/*
    Time Complexity  : O(N)
    Space Complexity : O(N)

    Where N is the total number of nodes in the binary tree.
*/
vector<int> zigZagTraversal(BinaryTreeNode<int> *root)
{
    vector<int> result; // Create an empty vector to store the traversal result.

    if (root == NULL)
        return result; // If the root is null, return the empty result vector.

    stack<BinaryTreeNode<int> *> s1; // Create stack s1 to store nodes for left-to-right traversal.
    stack<BinaryTreeNode<int> *> s2; // Create stack s2 to store nodes for right-to-left traversal.

    s1.push(root); // Push the root node into s1.

    while (!s1.empty() || !s2.empty())
    {
        while (!s1.empty()) // Perform left-to-right traversal.
        {
            BinaryTreeNode<int> *temp = s1.top();
            s1.pop();
            result.push_back(temp->data); // Add the node's data to the result vector.

            if (temp->left)
                s2.push(temp->left); // Push the left child into s2 if it exists.
            if (temp->right)
                s2.push(temp->right); // Push the right child into s2 if it exists.
        }

        while (!s2.empty()) // Perform right-to-left traversal.
        {
            BinaryTreeNode<int> *temp = s2.top();
            s2.pop();
            result.push_back(temp->data); // Add the node's data to the result vector.

            if (temp->right)
                s1.push(temp->right); // Push the right child into s1 if it exists.
            if (temp->left)
                s1.push(temp->left); // Push the left child into s1 if it exists.
        }
    }

    return result; // Return the resulting zigzag traversal.
}


```

# Approach
```cpp

/*
    Time Complexity  : O(N)
    Space Complexity : O(N)

    Where N is the total number of nodes in the binary tree.
*/

#include <deque>

vector<int> zigZagTraversal(BinaryTreeNode<int> *root) {
    // Declare an empty array answer to store zigzag traversal
    vector<int> answer;

    // Base case
    if (root == NULL) {
        return answer;
    }

    // Declare an empty deque and push back root to it
    deque<BinaryTreeNode<int>*> d;
    d.push_back(root);

    // Declare a variable level to get current level and initialize it to 1
    int level = 1;

    // Run a loop until deque is not empty
    while (!d.empty())
    {
        // Size of deque i.e. denotes no. of nodes in current level
        int n = d.size();

        // Run a loop until nodes in the current level are greater than zero
        while (n--)
        {
            // In current level is odd
            if (level % 2 == 1)
            {

                // pop the front node from deque and add its data to answer
                BinaryTreeNode<int>* backNode = d.front();
                d.pop_front();
                answer.push_back(backNode->data);

                // Push back left and right child of popped node to deque
                if (backNode->left != NULL)
                {
                    d.push_back(backNode->left);
                }
                if (backNode->right != NULL)
                {
                    d.push_back(backNode->right);
                }

            }
            // If current level is even
            else
            {
                // Pop back node from deque and add its data to answer
                BinaryTreeNode<int>* backNode = d.back();
                d.pop_back();
                answer.push_back(backNode->data);

                // Push right and left child of popped node to front of deque
                if (backNode->right != NULL)
                {
                    d.push_front(backNode->right);
                }
                if (backNode->left != NULL)
                {
                    d.push_front(backNode->left);
                }
            }
        }

        // Increment level by 1
        level++;
    }
    return answer;
}


```