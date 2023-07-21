# Merge Two Sorted Linked Lists

```cpp

#include <bits/stdc++.h>

/************************************************************

    Following is the linked list node structure.
    
    template <typename T>
    class Node {
        public:
        T data;
        Node* next;

        Node(T data) {
            next = NULL;
            this->data = data;
        }

        ~Node() {
            if (next != NULL) {
                delete next;
            }
        }
    };

************************************************************/


Node<int>* sortTwoLists(Node<int>* first, Node<int>* second)
{
    if (first == nullptr) {
        return second;
    }

    if (second == nullptr) {
        return first;
    }

    if (first->data > second->data) {
        std::swap(first, second);
    }

    Node<int>* res = first;

    while (first->next && second) {
        if (first->next->data > second->data) {
            Node<int>* temp = first->next;
            first->next = second;
            second = second->next;
            first->next->next = temp;
        }
        first = first->next;
    }

    if (second) {
        first->next = second;
    }

    return res;
}



```