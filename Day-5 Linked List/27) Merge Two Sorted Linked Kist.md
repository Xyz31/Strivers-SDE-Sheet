# Merge Two Sorted Linked Lists


Sample Input 1:
2
1 4 5 -1
2 3 5 -1
7 8 -1
1 3 4 6 -1

Sample Output 1:
1 2 3 4 5 5 -1
1 3 4 6 7 8 -1

Explanation Of Input 1:
The first test case is already explained in the problem statement.

The second test case, the first list is: 7 -> 8 -> NULL
The second list is: 1 -> 3 -> 4 -> 6 -> NULL
The final list would be: 1 -> 3 -> 4 -> 6 -> 7 -> 8 -> NULL


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