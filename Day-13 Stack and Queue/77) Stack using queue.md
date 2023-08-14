# Stack using queue

```md



```

# Approach -I
```cpp

/*
    Time complexity: O(Q*N)
    For each push operation O(N); O(1) for all other operations.
    
    Space complexity: O(max(N1, N2))

    where Q is the number of queries, N denotes the maximum number of elements in the queue and
    ‘N1' and ‘N2’ denote the size of queues ‘q1’ and ‘q2’.
*/

#include <queue>

class Stack {
   public:
    queue<int> *q1, *q2;

    Stack() {  
        // Constructor.
        q1 = new queue<int>();
        q2 = new queue<int>();
    }

    int getSize() {
        // Return the size of the queue 'q1'.
        return q1->size();  
    }

    bool isEmpty() {
        return getSize() == 0;
    }

    void push(int data) {  
        // Simply enqueue data to q1.
        q1->push(data);
    }

    int pop() {
        if (isEmpty()) {
            return -1;
        }

        // Enqueue all the elements of q1 into q2 except the last one.
        while (q1->size() > 1) {  
            q2->push(q1->front());
            q1->pop();
        }

        // Last element of q1 is our answer.
        int ans = q1->front();  
        q1->pop();

        // Swap q1 and q2.
        queue<int> *temp = q1;  
        q1 = q2;
        q2 = temp;

        return ans;
    }

    int top() {
        if (isEmpty()) {
            return -1;
        }

        // Enqueue all the elements of q1 into q2 except the last one.
        while (q1->size() > 1) {  
            q2->push(q1->front());
            q1->pop();
        }

        // Last element of q1 is our answer.
        int ans = q1->front();  
        q1->pop();
        // Enqueue the top to q2.
        q2->push(ans);  

        queue<int> *temp = q1;
        q1 = q2;
        q2 = temp;

        return ans;
    }
};

```

# Approach -II

```cpp

#include <bits/stdc++.h>

class Stack {
    queue<int> q1; // Queue to store stack elements

public:
    Stack() {} // Default constructor

    // Function to get the size of the stack
    int getSize()
    {
        return q1.size();
    }

    // Function to check if the stack is empty
    bool isEmpty()
    {
        return q1.empty();
    }

    // Function to push an element onto the stack
    void push(int element)
    {   
        // Optimized implementation using 1 queue
        
        int sz = q1.size(); // Get the current size of the queue
        
        // Add the new element to the back of the queue
        q1.push(element);

        // Reorder the elements in the queue to maintain stack ordering
        // by moving the newly added element to the front
        for (int i = 0; i < sz; i++) {
            int temp = q1.front(); // Store the front element
            q1.pop(); // Remove the front element
            q1.push(temp); // Add the front element to the back
        }
    }

    // Function to remove and return the top element from the stack
    int pop()
    {
        if (!isEmpty()) {
            int temp = q1.front(); // Get the front element (top of the stack)
            q1.pop(); // Remove the front element
            return temp; // Return the top element
        }
        return -1; // Return -1 if the stack is empty
    }

    // Function to get the top element from the stack without removing it
    int top()
    {
        if (!isEmpty()) {
            return q1.front(); // Return the front element (top of the stack)
        }
        return -1; // Return -1 if the stack is empty
    }
};


```