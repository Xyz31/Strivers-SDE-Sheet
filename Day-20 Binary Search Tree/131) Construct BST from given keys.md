# Construct BST from given keys


# Approach - I Recursive Approach
```cpp

/*
    Time Complexity: O(N)
    Space Complexity: O(log(N))

    where 'N' is the total number of elements in the given array.
*/

// Recursive function that return the root node of a subtree, for particular array segment.
TreeNode<int>* convert (vector<int> &arr, int start, int end)
{
    // Base case.
    if(start > end)
    {
        return NULL;
    }

    else
    {
        // Find 'mid' index of array and make it root node. 
        int mid = (start+end)/2;
        TreeNode<int>* rootNode = new TreeNode<int>(arr[mid]);

        // Call 'convert' function for the left part of array to make leftSubtree of root node.
        rootNode -> left = convert(arr,start,mid-1);

        // Call 'convert' function for the right part of array to make rightSubtree of root node.
        rootNode -> right = convert(arr,mid+1,end);

        // Return the rootNode.
        return rootNode;
    }
}


TreeNode<int>* sortedArrToBST (vector<int> &arr, int n)
{
    // Call the recursive function to convert array into tree.
    TreeNode<int>* root = convert(arr, 0, n-1);

    // Return the root node of tree.
    return root;
}

```

# Approach - II Iterative Approach
```cpp

/*
    Time Complexity: O(N)
    Space Complexity: O(log(N))

    where 'N' is the total number of elements in the given array.
*/

// NodeData struct to store root node of subtree and their respective range in given array.
struct nodeData
{
    TreeNode<int> *node;

    // Low and high are left and right range for given 'arr'.
    int low, high;

    nodeData(TreeNode<int>* root, int left, int right)
    {
        node = root;
        low = left ;
        high = right;
    }
};


TreeNode<int>* sortedArrToBST (vector<int> &arr, int n)
{
    /*
        Initialise a root node with 'val' = -1 and range [ 0:n-1 ] and push it into a stack data structure.
        Later on we will update its 'val' to arr['mid'], where 'mid' is middle index of range [0:n-1].
    */
    TreeNode<int>* root = new TreeNode<int> (-1);
    stack<nodeData> st;

    nodeData node = nodeData(root, 0, n - 1);
    st.push(node); 

    while (st.empty() == false)
    {
        nodeData curNode = st.top();
        st.pop();

        // Find 'mid' for the currNode and update node with arr[mid].
        int mid = curNode.low + (curNode.high - curNode.low) / 2;
        curNode.node -> val = arr[mid];

        // Push the left part of array, that makes left subtree of current node.
        if (curNode.low < mid)
        {
            curNode.node -> left = new TreeNode<int>(-1);

            node = nodeData(curNode.node -> left, curNode.low, mid - 1);
            st.push(node);
        }

        // Push the right part of array, that makes right subtree of current node.
        if (curNode.high > mid) 
        {
            curNode.node -> right = new TreeNode<int>(-1);
            
            node = nodeData(curNode.node -> right, mid+1, curNode.high);
            st.push(node);
        }
    }

    // Return root of tree.
    return root;
}


```