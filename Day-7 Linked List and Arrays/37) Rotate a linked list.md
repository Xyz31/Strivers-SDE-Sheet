# Rotate a linked list


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