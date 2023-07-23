# Queue Using Stack

# Approach -I
```cpp

/*
    Time complexity: O(N * Q)
        For enQueue(): O(N) 
        For deQueue(): O(1) 
        For peek(): O(1)
        For isEmpty(): O(1)

    Space Complexity : O(N)

    Where 'N' is the maximum number of elements that are in the stack at any time.
    Where 'Q' is the total number of queries which are performed.
*/

#include <stack>

class Queue {
    stack<int> *s1;
    stack<int> *s2;
public:
    Queue() {
        s1 = new stack<int>();
        s2 = new stack<int>();

    }
    // EnQueue item to the queue.
    void enQueue(int val) {
        // Move all elements from s1 to s2.
        while (!s1->empty()) {
            // To insert a value, first whole of the s1 is transferred to s2, then the new element is inserted in s1.
            s2->push(s1->top());  
            s1->pop();
        }

        // Push item into s1.
        s1->push(val);

        // Push everything back to s1.
        while (!s2->empty()) {
            s1->push(s2->top());    
            s2->pop();
        }


    }

    // Dequeue an item from the queue.
    int deQueue() {
        // If first stack is empty.
        if(s1->empty()) {
            return -1;
        }

        // Return top of s1.
        int tp = s1->top();
        s1->pop();
        return tp;
    }

    // Returns the Front element of the queue.
    int peek() {
        if (s1->empty()) {
            return -1;
        }

        return s1->top();
    }

    // Whether the queue is empty or not.
    bool isEmpty() {
        return (s1->empty());
    }

};

```

# Approach -II

```cpp


class Queue {
    stack<int> input, output; // Stacks to store queue elements

public:
    Queue(){} // Default constructor

    // Function to enqueue an element
    void enQueue(int val)
    {
        input.push(val); // Push the element to the input stack
    }

    // Function to dequeue an element
    int deQueue()
    {
        if (output.empty()) { // If the output stack is empty
            // Move elements from the input stack to the output stack in reverse order
            while (!input.empty()) {
                output.push(input.top()); // Push the top element from the input stack to the output stack
                input.pop(); // Pop the top element from the input stack
            }
        }

        if (output.empty()) return -1; // If both stacks are empty, return -1 (queue is empty)

        int val = output.top(); // Get the top element from the output stack (front of the queue)
        output.pop(); // Pop the top element from the output stack (remove the front element)
        return val; // Return the front element of the queue
    }

    // Function to peek at the front element of the queue
    int peek()
    {
        if (output.empty()) { // If the output stack is empty
            // Move elements from the input stack to the output stack in reverse order
            while (!input.empty()) {
                output.push(input.top()); // Push the top element from the input stack to the output stack
                input.pop(); // Pop the top element from the input stack
            }
        }

        if (output.empty()) return -1; // If both stacks are empty, return -1 (queue is empty)

        return output.top(); // Return the top element from the output stack (front of the queue)
    }

    // Function to check if the queue is empty
    bool isEmpty()
    {
        return input.empty() && output.empty(); // Return true if both input and output stacks are empty
    }
};


/*
class Queue {
    // Define the data members(if any) here.
    
    public:
    Queue() {
        // Initialize your data structure here.
    }

    void enQueue(int val) {
        // Implement the enqueue() function.
    }

    int deQueue() {
        // Implement the dequeue() function.
    }

    int peek() {
        // Implement the peek() function here.
    }

    bool isEmpty() {
        // Implement the isEmpty() function here.
    }
};
*/


```