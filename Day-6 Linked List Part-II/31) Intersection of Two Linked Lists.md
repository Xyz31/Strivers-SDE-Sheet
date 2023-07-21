# Intersection of Two Linked Lists


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