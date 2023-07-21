# Delete A Given Node

```cpp

#include <bits/stdc++.h>

/****************************************************************

    Following is the class structure of the LinkedListNode class:

    template <typename T>
    class LinkedListNode
    {
    public:
        T data;
        LinkedListNode<T> *next;
        LinkedListNode(T data)
        {
            this->data = data;
            this->next = NULL;
        }
    };

*****************************************************************/

void deleteNode(LinkedListNode<int> * node){
if (node == nullptr || node->next == nullptr) {
        // If the node is null or the last node, we cannot delete it.
        return;
    }

    // Get the next node.
    LinkedListNode<int>* nextNode = node->next;
    // Copy the data and next pointer from the next node to the current node.

    node->data = nextNode->data;
    node->next = nextNode->next;
    
    // Delete the next node.
    delete nextNode;
}

```