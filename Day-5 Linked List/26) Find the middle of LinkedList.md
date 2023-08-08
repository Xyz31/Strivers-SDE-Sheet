# Find the middle of LinkedList

Sample Input 1 :
5
1 2 3 4 5

Sample Output 1 :
3 4 5

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

// Node *findMiddle(Node *head) {
    // Write your code here

    
Node* findMiddle(Node* head) {
    // Initialize two pointers, slow and fast, pointing to the head
    Node* slow = head;
    Node* fast = head;

    // Traverse the linked list with fast pointer moving two steps at a time
    // and slow pointer moving one step at a time
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;      // Move slow pointer one step forward
        fast = fast->next->next; // Move fast pointer two steps forward
    }

    // At this point, the fast pointer has reached the end of the linked list
    // and the slow pointer is pointing to the middle node (or middle-left node
    // in case of an even number of nodes)

    return slow; // Return the middle node
}




```