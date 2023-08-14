# Serialize and deserialize Binary Tree


```md



```
 
# Approach - I Level order Traversal Approach
```cpp

/*
    Time Complexity - O(N)
    Space Complexity - O(N)

    Where N is the number of nodes in the Binary Tree.
*/

#include <string>

string serializeTree(TreeNode<int> *root)
{
    
    //    Intialize serialized as an empty string
    string serialized = "";

    //    Queue for level order traversal
    queue<TreeNode<int> *> level;
    level.push(root);

    while (level.empty() == false)
    {
        
        //    Pop the Node at the front
        TreeNode<int> *curr = level.front();
        level.pop();

        //    If the current node is not null.
        if (curr != NULL)
        {
            
            //    Add the value of the curr node to the serialized string.
            serialized.append(to_string(curr->data));
            serialized.push_back(',');

            //    Push the left and the right child nodes in the queue.
            level.push(curr->left);
            level.push(curr->right);
        }

        //    If the current node is null
        else
        {
            
            //    Add -1 to the serialized string.
            serialized.append("-1,");
        }
    }

    //    Return the serialized binary tree.
    return serialized;
}

TreeNode<int> *deserializeTree(string &serialized)
{

    //    Pointer for reading elements from the serialized binary tree.
    int ptr = 0;
    string firstVal = "";

    //    Read the first value from the string.
    while (ptr < serialized.length() && serialized[ptr] != ',')
    {
        firstVal.push_back(serialized[ptr]);
        ptr++;
    }
    ptr++;
    int val = stoi(firstVal);

    //    If the first value if -1 then return null.
    if (val == -1)
    {
        return NULL;
    }

    //    Create a new root node.
    TreeNode<int> *root = new TreeNode<int>(val);

    //    Queue for level order traversal.
    queue<TreeNode<int> *> level;

    //    Push the root node into the queue.
    level.push(root);

    while (level.empty() == false)
    {
        
        //    Pop the front node from the queue.
        TreeNode<int> *curr = level.front();
        level.pop();

        string leftChild = "";

        //    Read the value of the left child.
        while (ptr < serialized.length() && serialized[ptr] != ',')
        {
            leftChild.push_back(serialized[ptr]);
            ptr++;
        }
        ptr++;
        string rightChild = "";

        //    Read the value of the right child.
        while (ptr < serialized.length() && serialized[ptr] != ',')
        {
            rightChild.push_back(serialized[ptr]);
            ptr++;
        }
        ptr++;

        int leftChildValue = stoi(leftChild);
        int rightChildValue = stoi(rightChild);

        //    If the left child node is not null
        if (leftChildValue != -1)
        {
            
            //    Create new left child node.
            TreeNode<int> *leftNode = new TreeNode<int>(leftChildValue);
            curr->left = leftNode;

            //    Push the left child into the queue.
            level.push(curr->left);
        }

        //    If the right child is not null
        if (rightChildValue != -1)
        {
            
            //    Create new right child node.
            TreeNode<int> *rightNode = new TreeNode<int>(rightChildValue);
            curr->right = rightNode;

            //    Push the right child into the queue.
            level.push(curr->right);
        }
    }

    //    Return the root of deserialized the binary tree.
    return root;
}

```

# Approach - II
```cpp



```