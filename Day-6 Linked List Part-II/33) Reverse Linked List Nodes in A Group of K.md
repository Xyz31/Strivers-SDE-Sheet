# Reverse Linked List Nodes in A Group of K.


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