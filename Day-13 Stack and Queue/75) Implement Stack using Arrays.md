# Implement Stack using Arrays


```md



```

```cpp

#include <bits/stdc++.h> 
// Stack class.



class Stack {
public:
    stack<int> s;
    int size;

    Stack(int capacity) {
        // Write your code here.
        size = capacity;
    }

    void push(int num) {
        // Write your code here.
        if (s.size() < size) {
            s.push(num);
        }
    }

    int pop() {
        // Write your code here.
        if (s.empty()) {
            return -1;
        }
        int k = s.top();
        s.pop();
        return k;
    }

    int top() {
        // Write your code here.
        if (s.empty()) {
            return -1;
        }
        return s.top();
    }

    int isEmpty() {
        // Write your code here.
        return s.empty();
    }

    int isFull() {
        // Write your code here.
        return s.size() == size;
    }
};

```