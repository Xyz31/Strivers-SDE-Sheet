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