# Cycle Detection in a Singly Linked List


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

bool detectCycle(Node *head)
{
	//	Write your code here

        // Check if the linked list is empty or has only one node.
    // If it does, there can't be a cycle, so return false.
    if (head == NULL || head->next == NULL) {
        return false;
    }

    // Initialize two pointers, slow and fast, to the head of the linked list.
    Node *slow = head;
    Node *fast = head;

    // Traverse the linked list using the slow and fast pointers.
    // The fast pointer moves twice as fast as the slow pointer.
    // If there is a cycle, the fast pointer will eventually catch up to the slow pointer.

    while (fast != NULL && fast->next != NULL) {
        // Move the slow pointer one step at a time.
        slow = slow->next;

        // Move the fast pointer two steps at a time.
        fast = fast->next->next;

        // Check if the fast pointer reaches the end of the linked list or becomes NULL.
        // If it does, it means there is no cycle in the linked list, so return false.
        if (fast == NULL || fast->next == NULL) {
            return false;
        }

        // If the fast pointer becomes equal to the slow pointer, it indicates a cycle in the linked list.
        // Return true in this case.
        if (fast == slow) {
            return true;
        }
    }

    // The while loop terminates if the fast pointer reaches the end of the linked list,
    // indicating that there is no cycle in the linked list. Return false in this case.
    return false;
}

```