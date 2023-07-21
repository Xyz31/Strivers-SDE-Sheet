# Check Linked list is palindrome or not

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
bool isPalindrome(LinkedListNode<int> *head) {
    // Check for empty list or single node (considered a palindrome)
    if (head == nullptr || head->next == nullptr) {
        return true;
    }

    LinkedListNode<int> *fast = head;
    LinkedListNode<int> *slow = head;
    LinkedListNode<int> *prev = nullptr;

    // Find the middle node using the fast and slow pointers
    while (fast != nullptr && fast->next != nullptr) {
        fast = fast->next->next;  // Move fast pointer two steps ahead
        LinkedListNode<int> *next = slow->next;
        slow->next = prev;  // Reverse the first half of the list
        prev = slow;
        slow = next;  // Move slow pointer one step ahead
    }

    // Handle odd number of nodes by moving slow pointer forward
    if (fast != nullptr) {
        slow = slow->next;
    }

    // Compare the reversed second half with the first half
    while (prev != nullptr && slow != nullptr) {
        if (prev->data != slow->data) {
            return false;  // Not a palindrome
        }
        prev = prev->next;
        slow = slow->next;
    }

    return true;  // Palindrome
}

```