# Remove N-th node from back of LinkedList

## code 

```cpp

/*
Following is the class structure of the Node class:

class Node
{
public:
    int data;
    Node *next;
    Node()
    {
        this->data = 0;
        next = NULL;
    }
    Node(int data)
    {
        this->data = data; 
        this->next = NULL;
    }
    Node(int data, Node* next)
    {
        this->data = data;
        this->next = next;
    }
};
*/
Node* removeKthNode(Node* head, int K)
{
    Node* fast, *slow; // Pointers for traversal
    fast = head;
    slow = head;

    for (int i = 0; i < K; i++) {
        fast = fast->next; // Move the 'fast' pointer 'K' nodes ahead
    }

    if (fast == NULL) {
        return head->next; // If 'fast' reaches the end, remove the first node (K = length of the list)
    }

    while (fast->next != NULL) {
        slow = slow->next; // Move 'slow' one node ahead
        fast = fast->next; // Move 'fast' to the next node
    }

    // 'slow' is now pointing to the node just before the Kth node
    slow->next = slow->next->next; // Skip the Kth node by updating 'slow->next'

    return head; // Return the modified linked list
}


```