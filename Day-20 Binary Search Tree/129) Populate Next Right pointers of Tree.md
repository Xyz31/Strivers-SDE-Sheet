# Populate Next Right pointers of Tree


# Approach - I Level Order Traversal or BFS.
```cpp

/*
    Time complexity: O(N)
    Space complexity: O(N)

    Where 'N' is the number of nodes in a binary tree.
*/

#include <queue>

void connectNodes(BinaryTreeNode<int> *root) {

    // Create queue and enqueue address of root in it.
    queue< BinaryTreeNode<int>* > que;
    que.push(root);

    // Number of nodes in current level.
    int nodesCount = 1;

    while(!que.empty()) {
        BinaryTreeNode<int> *previous = NULL;

        // Traversing over nodes of current level.
        while(nodesCount > 0) {
            if(previous != NULL) {
                previous->next = que.front();
            }
            previous = que.front();

            // Pushing left and right child of current node in queue. 
            if(que.front()->left != NULL) {
                que.push(que.front()->left);
            } 
            if(que.front()->right != NULL) {
                que.push(que.front()->right);
            }
            que.pop();
            nodesCount--;
        }
        
        // Updating number of nodes in current level. 
        nodesCount = que.size();
    }
}

```

# Approach - II Optimized Level Order Traversal
```cpp

/*
    Time complexity: O(N)
    Space complexity: O(1)
    
    Where 'N' is the number of nodes in a binary tree.
*/

void connectNodes(BinaryTreeNode<int> *root) {

    // Keep the address of the first node of the current level.
    BinaryTreeNode<int> *startNode = root;

    while(startNode != NULL) {

        BinaryTreeNode<int> *ptr = startNode;
        BinaryTreeNode<int> *previous = NULL;
        startNode = NULL;
        
        // Traversing over nodes of current level and populating 'next' pointer of nodes of next level.
        while(ptr != NULL) {

            if(ptr->left != NULL) {

                if(previous != NULL) {
                    previous->next = ptr->left;
                }

                // Update 'startNode' with first node of next level if not already done.
                if(startNode == NULL) {
                    startNode = ptr->left;
                }

                // Update previous pointer
                previous = ptr->left;
            }

            if(ptr->right != NULL) {

                if(previous != NULL) {
                    previous->next = ptr->right;
                }

                // Update 'startNode' with first node of next level if not already done.
                if(startNode == NULL) {
                    startNode = ptr->right;
                }

                // Update previous pointer.
                previous = ptr->right;
            }

            ptr = ptr->next;
        }
    }
}

```