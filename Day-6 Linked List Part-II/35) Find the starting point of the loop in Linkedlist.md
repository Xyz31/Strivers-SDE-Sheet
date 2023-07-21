# Find the starting point of the loop in Linkedlist


```cpp

/****************************************************************

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


*****************************************************************/
Node *firstNode(Node *head)
{
    if (head == nullptr || head->next == nullptr) {
        return nullptr;  // No cycle exists
    }

    Node *slow = head;
    Node *fast = head;

    // Detect the cycle using the fast and slow pointers
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;

        if (slow == fast) {
            break;  // Cycle detected
        }
    }

    // If there is no cycle, return nullptr
    if (fast == nullptr || fast->next == nullptr) {
        return nullptr;
    }

    // Move slow pointer back to the head
    slow = head;


    /*
    If a cycle is detected, the slow pointer is moved back to the head of the linked list. 
    This step is necessary to find the first node of the cycle.
    */
    
    // Move slow and fast pointers at the same pace until they meet at the start of the cycle
    while (slow != fast) {
        slow = slow->next;
        fast = fast->next;
    }

    return slow;  // Return the first node of the cycle
}

```