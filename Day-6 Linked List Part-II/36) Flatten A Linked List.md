# Flatten A Linked List

Sample Input 1 :
4
3
1 2 3
3
8 10 15
2
18 22
1
29


Sample Output 1 :
1 2 3 8 10 15 18 22 29


Explanation For Sample Input 1:
The given linked list is 

Therefore after flattening the list will become-
1 -> 2 -> 3 -> 8 -> 10 -> 15 -> 18 -> 22 -> 29 ->null

## code 
```cpp

/*
 * Definition for linked list.
 * class Node {
 *  public:
 *		int data;
 *		Node *next;
 * 		Node *child;
 *		Node() : data(0), next(nullptr), child(nullptr){};
 *		Node(int x) : data(x), next(nullptr), child(nullptr) {}
 *		Node(int x, Node *next, Node *child) : data(x), next(next), child(child) {}
 * };
 */
#include <queue>

// Merge two linked lists based on their data values
Node* merge(Node* first, Node* second) {
    // If the first list is NULL, return the second list
    if (first == NULL) {
        second->next = nullptr;
        return second;
    }

    // If the second list is NULL, return the first list
    if (second == NULL) {
        first->next = nullptr;
        return first;
    }

    Node* merged = NULL;

    // Compare the data values of the first and second nodes
    if (first->data < second->data) {
        merged = first;
        // Recursively merge the remaining nodes of the first list with the second list
        merged->child = merge(first->child, second);
    } else {
        merged = second;
        // Recursively merge the remaining nodes of the second list with the first list
        merged->child = merge(first, second->child);
    }

    merged->next = nullptr; // Set the next pointer of the merged list to NULL
    return merged; // Return the head of the merged list
}

// Flatten a linked list with child pointers
Node* flattenLinkedList(Node* head) {
    // Base case: If the head is NULL or the last node, return the head itself
    if (head == NULL || head->next == NULL) {
        return head;
    }

    // Recursively flatten the next node
    head->next = flattenLinkedList(head->next);

    // Merge the current node with the flattened next node
    head = merge(head, head->next);

    return head; // Return the head of the fully flattened list
}

```