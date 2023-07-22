# Reverse a LinkedList

## code 

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

LinkedListNode<int> *reverseLinkedList(LinkedListNode<int> *head) 
{
    // Write your code here

    LinkedListNode<int> *prev = nullptr;
    LinkedListNode<int> *cur = head;
    LinkedListNode<int> *next = nullptr;

    while (cur != nullptr) {
        next = cur->next;      // Store the next node
        cur->next = prev;      // Reverse the pointer
        prev = cur;            // Move prev to the current node
        cur = next;            // Move cur to the next node
    }

    return prev;               // Return the new head (prev)

}

```