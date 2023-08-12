
 # Day 6- Linked List
 🔥
 # Reverse a LinkedList

Sample Input 1 :\
1\
1 2 3 4 5 6 -1


Sample Output 1 :\
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

Sample Input 1 :\
5\
1 2 3 4 5

Sample Output 1 :\
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


Sample Input 1:\
2\
1 4 5 -1\
2 3 5 -1\
7 8 -1\
1 3 4 6 -1

Sample Output 1:\
1 2 3 4 5 5 -1\
1 3 4 6 7 8 -1

Explanation Of Input 1:\
The first test case is already explained in the problem statement.

The second test case, the first list is: 7 -> 8 -> NULL
The second list is: 1 -> 3 -> 4 -> 6 -> NULL
The final list would be: 1 -> 3 -> 4 -> 6 -> 7 -> 8 -> NULL

## code
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

Sample Input 1 :\
6 3\
1 2 3 4 5 6 

Sample Output 1 :\
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

Sample Input 1 :\
3\
1 2 3\
3\
4 5 6


Sample Output 1 :\
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

Sample Input 1:\
 2\
2 5 7 10 -1\
7\
-8 3 4 -2 1 -1 \
4



Sample Output 1:\
2 5 10 -1\
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

# Intersection of Two Linked Lists

Sample Input 1 :\
4 1 -1\
5 6 -1\
8 -1

Sample Output 1 :\
8

Explanation For Sample Input 1:
As shown in the diagram, the node with data is 8, at which merging starts
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

Node* findIntersection(Node *firstHead, Node *secondHead)
{
    //Write your code here

    if(firstHead == NULL || secondHead == NULL){
        return {};
    }

    // Initialize two pointers, temp1 and temp2, to the heads of the linked lists.
Node * temp1 = firstHead;
Node *temp2 = secondHead;

// Traverse both linked lists until temp1 and temp2 become equal or both reach the end of their respective lists.
// If the linked lists have an intersection, the loop will eventually find the common node.
while(temp1 != temp2){
    // If temp1 reaches the end of the first list, reset it to the head of the second list.
    temp1 = temp1 == NULL ? secondHead : temp1->next;
    // If temp2 reaches the end of the second list, reset it to the head of the first list.
    temp2 = temp2 == NULL ? firstHead : temp2->next;
}

// Return the node where temp1 and temp2 are equal, which is the intersection point.
// If there is no intersection, both temp1 and temp2 will become NULL, and it will return NULL.
return temp1;


}


```

# Cycle Detection in a Singly Linked List

Sample Input 1 :\
1 2 3 4 -1\
1

Sample Output 1 :\
true

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
# Reverse Linked List Nodes in A Group of K.

Sample Input 1:\
1 2 3 4 5 6 7 8 9 10 11 -1\
3\
2 3 4

Sample Output 1:\
2 1 5 4 3 9 8 7 6 10 11 -1

Explanation Of The Sample Output 1:
For the given input, the block sizes are 2, 3 and 4 respectively. First, we reverse 2 elements (1->2 becomes 2->1), then the next 3 elements (3->4->5 becomes 5->4->3) and lastly the next 4 elements (6->7->8->9 becomes 9->8->7->6). Thus, the final modified list becomes 2->1->5->4->3->9->8->7->6->10->11. 

```cpp

#include <bits/stdc++.h>

/****************************************************************

    Following is the class structure of the Node class:

        class Node
        {
        public:
	        int data;
	        Node *next;
	        Node(int data)
	        {
		        this->data = data;
		        this->next = NULL;
	        }
        };

*****************************************************************/


// Function to reverse a linked list up to 'k' nodes
Node *reverseLinkedList(Node *head, int k)
{
    Node *prev = NULL;
    Node *current = head;
    Node *next = NULL;

    int count = 0;
    while (current != NULL && count < k)
    {
        next = current->next;
        current->next = prev;
        prev = current;
        current = next;
        count++;
    }

    if (next != NULL)
    {
        head->next = reverseLinkedList(next, k); // Recursively reverse the remaining list
    }

    return prev; // Return the new head of the reversed list
}

// Function to perform the desired reverse operation on the linked list
Node *getListAfterReverseOperation(Node *head, int n, int b[])
{
    Node *newHead = head;
    Node *prevTail = NULL;
    int i = 0;

    while (i < n && newHead != NULL)
    {
        int blockSize = b[i];
        Node *blockHead = newHead;
        Node *blockTail = NULL;
        int count = 0;

        // Traverse 'blockSize' nodes to identify the block to be reversed
        while (count < blockSize && newHead != NULL)
        {
            blockTail = newHead;
            newHead = newHead->next;
            count++;
        }

        if (blockTail != NULL)
        {
            blockTail->next = NULL; // Disconnect the block from the rest of the list

            if (prevTail != NULL)
            {
                prevTail->next = reverseLinkedList(blockHead, blockSize); // Reverse the block and connect it to the previous block
            }
            else
            {
                head = reverseLinkedList(blockHead, blockSize); // Reverse the first block and update the head
            }

            prevTail = blockHead; // Update the previous tail to the current block head
        }

        i++; // Move to the next block size
    }

    if (prevTail != NULL)
    {
        prevTail->next = newHead; // Connect the remaining list, if any
    }

    return head; // Return the modified linked list
}


```

# Check Linked list is palindrome or not

Sample Input 1 :\
2\
1 2 3 4 5 6 -1\
1 2 1 -1

Sample Output 1 :\
false\
true

Explanation For Sample 1:
For the first test case, it is not a palindrome because Linked List doesn't have the same order of elements when traversed forwards and backwards​.

For the second test case, it is a palindrome linked list because a Linked List has the same order of elements when traversed forwards and backwards​.

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

# Find the starting point of the loop in Linkedlist


Sample Input 1 :\
1 2 3 4 -1\
1

Sample Output 1 :\
1

## code
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

# Flatten A Linked List

Sample Input 1 :\
4\
3\
1 2 3\
3\
8 10 15\
2\
18 22\
1\
29


Sample Output 1 :\
1 2 3 8 10 15 18 22 29


Explanation For Sample Input 1:\
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

# Rotate a linked list

Sample Input 1 :\
6\
1 2 3 4 5 6\
2


Sample Output 1 :\
5 6 1 2 3 4


Explanation For Sample Input 1 :\
For the first test case, after 1st clockwise rotation the modified linked list will be :\
6->1->2->3->4->5\
After, 2nd clockwise rotated the modified linked list will be : \
5->6->1->2->3->4.\
Thus the output is: \
5 6 1 2 3 4.


## code
```cpp

/**

 * Definition for singly-linked list.
 * class Node {
 * public:
 *     int data;
 *     Node *next;
 *     Node() : data(0), next(nullptr) {}
 *     Node(int x) : data(x), next(nullptr) {}
 *     Node(int x, Node *next) : data(x), next(next) {}
 * };


 */
Node *rotate(Node *head, int k) {
     // Rotate the linked list by k positions to the right

     if(k==0){
          return head;
     }

     Node *fast = head;
     Node *last = head;
     int count = 0;

     // Find the last node and count the number of nodes in the linked list
     while(fast->next != nullptr){
          fast = fast->next;
          count++;
     }

     // Make the last node point to the head to create a circular linked list
     fast->next = head;
     count++;

     // Calculate the actual number of rotations needed
     k = k % count;
     int t = count - k;

     Node *first = head;
     Node *prev;

     // Traverse to the node that will become the new head after rotation
     while(t){
          prev = first;
          first = first->next;
          t--;
     }

     // Set the previous node's next pointer to null to break the circular linked list
     prev->next = nullptr;

     // Return the new head of the rotated linked list
     return first;
}


```

# Copy Linked List with Random Pointer

Sample Input 1:\
1\
1 2 2 0 3 4 4 4 5 1 -1

Sample Output 1:\
true

Explanation Of Sample Input 1:\
For the first test case, “true” will be printed if the linked list is successfully cloned.

## code
```cpp

#include <bits/stdc++.h>

/*************************************************************

    Following is the LinkedListNode class structure

    template <typename T>   
    class LinkedListNode
    {
        public:
        T data;
        LinkedListNode<T> *next;
        LinkedListNode<T> *random;
        LinkedListNode(T data)
        {
            this->data = data;
            this->next = NULL;
        }
    };

*************************************************************/


/*
	Time complexity: O(N)
	Space complexity: O(1)

	Where 'N' is the number of nodes in the list.
*/

// This function clones a given linked list in O(1) space.
LinkedListNode<int> *cloneRandomList(LinkedListNode<int> *head)
{
    LinkedListNode<int> *curr = head, *temp = NULL;

    // Insert additional node after every node of original list.
    while (curr != NULL)
    {
        temp = curr->next;

        // Inserting node.
        curr->next = new LinkedListNode<int>(curr->data);
        curr->next->next = temp;
        curr = temp;
    }
    curr = head;

    // Adjust the random pointers of the newly added nodes.
    while (curr != NULL)
    {
        if (curr->next != NULL)
        {
            if (curr->random != NULL)
            {
                curr->next->random = curr->random->next;
            }
            else
            {
                curr->next->random = curr->random;
            }
        }

        // Move to the next newly added node by skipping an original node.
        if (curr->next != NULL)
        {
            curr = curr->next->next;
        }
        else
        {
            curr = curr->next;
        }
    }

    LinkedListNode<int> *original = head, *copy = NULL;

    if (head != NULL)
    {
        copy = head->next;
    }

    // Save the start of copied linked list.
    temp = copy;

    // Now separate the original list and copied list.
    while (original != NULL && copy != NULL)
    {
        if (original->next != NULL)
        {
            original->next = original->next->next;
        }

        if (copy->next != NULL)
        {
            copy->next = copy->next->next;
        }
        original = original->next;
        copy = copy->next;
    }
    return temp;

}

```