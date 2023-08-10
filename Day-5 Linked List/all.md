# Reverse a LinkedList

Sample Input 1 :
1
1 2 3 4 5 6 -1


Sample Output 1 :
6 5 4 3 2 1 -1


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

# Remove N-th node from back of LinkedList

Sample Input 1 :
6 3
1 2 3 4 5 6 

Sample Output 1 :
1 2 3 5 6

Explanation For Sample Input 1:
In the given linked list the node with data ‘4’ will be removed as this is the 3rd node from the end of the Linked List.

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

# Add two numbers as LinkedList

Sample Input 1 :
3
1 2 3
3
4 5 6


Sample Output 1 :
5 7 9


Explanation For Sample Input 1 :
'num1' represents the number 321 and 'num2' represents 654. Their sum is 975.

## code 

```cpp

/**
 * Definition of linked list:
 *
 * class Node {
 * public:
 *      int data;
 *      Node *next;
 *      Node() {
 *          this->data = 0;
 *          this->next = NULL;
 *      }
 *      Node(int data) {
 *          this->data = data;
 *          this->next = NULL;
 *      }
 *      Node (int data, Node *next) {
 *          this->data = data;
 *          this->next = next;
 *      }
 * };
 *
 *************************************************************************/

Node *addTwoNumbers(Node *num1, Node *num2)
{


    
    // Create a pointer to store the result list
    Node* result = nullptr;
    // Create a pointer to track the current position in the result list
    Node* current = nullptr;

    int carry = 0;

    // Iterate through the linked lists or continue if there is a carry
    while (num1 != nullptr || num2 != nullptr || carry != 0) {
        int sum = carry;

        // Add the values of the current nodes of num1 and num2, if available
        if (num1 != nullptr) {
            sum += num1->data;
            num1 = num1->next;
        }
        if (num2 != nullptr) {
            sum += num2->data;
            num2 = num2->next;
        }

        // Calculate the carry and digit for the current sum
        carry = sum / 10;
        int digit = sum % 10;

        // Create a new node with the digit
        Node* newNode = new Node(digit);

        // Connect the new node to the result list
        if (result == nullptr) {
            // If result list is empty, set the new node as the result
            result = newNode;
            current = result;
        } else {
            // Otherwise, append the new node to the current position and move the current pointer
            current->next = newNode;
            current = current->next;
        }
    }

    // Return the result list
    return result;

}

```

# Delete A Given Node

Sample Input 1:
2
2 5 7 10 -1
7
-8 3 4 -2 1 -1
4

Sample Output 1:
2 5 10 -1
-8 3 -2 1 -1

Explanation For Sample Input 1:
For the first test case, the given Linked List is

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

