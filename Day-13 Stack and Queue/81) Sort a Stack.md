# Sort a Stack

```md



```

```cpp

#include <bits/stdc++.h> 

/*
    Time Complexity: O(N^2)
    Space Complexity: O(N),

    where N is the number of elements in the stack.
*/


// Function to insert an element in its correct position in a sorted stack
void insertSorted(stack<int>& st, int x) {
    if (st.empty() || st.top() <= x) {
        // If the stack is empty or the top element is less than or equal to 'x', push 'x' onto the stack
        st.push(x);
    } else {
        // If the top element is greater than 'x', store the top element in 'temp'
        int temp = st.top();
        st.pop();
        // Recursively insert 'x' into the remaining stack
        insertSorted(st, x);
        // Push the stored element 'temp' back onto the stack
        st.push(temp);
    }
}

// Function to sort a stack using recursion
void sortStack(stack<int>& stack) {
    if (stack.empty())
        return;
    
    // Extract the top element of the stack
    int x = stack.top();
    stack.pop();
    
    // Recursively sort the remaining stack
    sortStack(stack);
    
    // Insert the extracted element 'x' back into the sorted stack
    insertSorted(stack, x);
}



```