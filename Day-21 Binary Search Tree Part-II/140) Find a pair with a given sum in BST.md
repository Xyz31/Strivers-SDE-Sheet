# Find a pair with a given sum in BST


# Approach - I Brute Force Approach
```cpp

/*
    Time Complexity: O(N ^ 2)
    Space Complexity: O(N)
    
    Where 'N' denotes the number of nodes in the BST.
*/

// Function to search the difference of current node's value and target 'k'. 
bool search(BinaryTreeNode<int> *root, BinaryTreeNode<int> *cur, int diff)
{
    if (root == NULL)
    {
        return false;
    }

    if (root -> data < diff)
    {
        return search(root -> right, cur, diff);
    }

    if (root -> data > diff)
    {
        return search(root -> left, cur, diff);
    }

    // This means that we have found the node having value equal to the diff.
    if (cur != root)
    {
        return true;
    }

    return false;
}

bool dfs(BinaryTreeNode<int> *root, int k, BinaryTreeNode<int> *cur)
{
    if (cur == NULL)
    {
        return false;
    }

    // Visit each node of BST and call the 'search' function.
    return (search(root, cur, k - cur->data) || dfs(root, k, cur -> left) || dfs(root, k, cur -> right));
}

bool pairSumBst(BinaryTreeNode<int> *root, int k)
{
    return dfs(root, k, root);
}



```

# Approach - II  Inorder Traversal
```cpp

/*
    Time Complexity: O(N)
    Space Complexity: O(N)
    
    Where 'N' denotes the number of nodes in the given BST
*/

#include<unordered_set>

bool helper(BinaryTreeNode<int> *root, int k, unordered_set<int> &hashSet)
{
    if (root == NULL)
    {
        return false;
    }

    // If the pair is found then return "true".
    if (hashSet.count(k - root->data))
    {
        return true;
    }

    // If the pair is not found then simply insert the root's data into the 'hashSet'.
    hashSet.insert(root -> data);

    // Recursively check for both left and right subtrees.
    return (helper(root -> left, k, hashSet) || helper(root -> right, k, hashSet));
}


bool pairSumBst(BinaryTreeNode<int> *root, int k)
{
    
    // Set to store the nodes.
    unordered_set<int> hashSet;
    
    return helper(root, k, hashSet);
}

```

# Approach - III Using Set
```cpp

/*
    Time Complexity: O(N)
    Space Complexity: O(N)
    
    Where 'N' denotes the number of nodes in the given BST
*/

#include<unordered_set>

bool helper(BinaryTreeNode<int> *root, int k, unordered_set<int> &hashSet)
{
    if (root == NULL)
    {
        return false;
    }

    // If the pair is found then return "true".
    if (hashSet.count(k - root->data))
    {
        return true;
    }

    // If the pair is not found then simply insert the root's data into the 'hashSet'.
    hashSet.insert(root -> data);

    // Recursively check for both left and right subtrees.
    return (helper(root -> left, k, hashSet) || helper(root -> right, k, hashSet));
}


bool pairSumBst(BinaryTreeNode<int> *root, int k)
{
    
    // Set to store the nodes.
    unordered_set<int> hashSet;
    
    return helper(root, k, hashSet);
}

```

# Approach - IV Two pointer technique

```cpp

/*
    Time Complexity: O(N)
    Space Complexity: O(N)
    
    Where 'N' denotes the number of nodes in the given BST
*/

#include<stack>

bool pairSumBst(BinaryTreeNode<int> *root, int k)
{
    
    /*
        Stack 'start' and 'end' to store the smaller and larger 
        values of BST respectively.
    */
    stack<BinaryTreeNode<int>*> start, end;

    BinaryTreeNode<int> *currNode = root;
    
    // Storing left values of BST in 'start'.
    while (currNode != NULL)
    {
        start.push(currNode);
        currNode = currNode -> left;
    }

    // Setting currNode again pointing to root.
    currNode = root;
    
    // Storing right values of BST in 'end'.
    while (currNode != NULL)
    {
        end.push(currNode);
        currNode = currNode -> right;
    }

    while (start.top() != end.top())
    {
        
        // Storing top node's value of 'start' stack in 'val1'.
        int val1 = start.top() -> data;
        
        // Storing top node's value of 'end' stack in 'val2'.
        int val2 = end.top() -> data;

        // If sum of 'val1' and 'val2' is equal to 'k' then return "true".
        if (val1 + val2 == k)
        {
            return true;
        }

        // Move to the next greatest closer value.
        if (val1 + val2 < k)
        {
            currNode = start.top() -> right;
            start.pop();
            
            while (currNode != NULL)
            {
                start.push(currNode);
                currNode = currNode -> left;
            }
        }

        // Move to the next smallest closer value.
        else
        {
            currNode = end.top() -> left;
            end.pop();

            while (currNode != NULL)
            {
                end.push(currNode);
                currNode = currNode -> right;
            }
        }
    }

    // If no two nodes is found, return false.
    return false;
}

```