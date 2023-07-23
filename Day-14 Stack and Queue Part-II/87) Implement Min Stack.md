# Implement Min Stack


```cpp

#include <bits/stdc++.h>

/*
    Time Complexity: O(N) 
    Space Complexity:O(N) 

    Where 'N' is the no. of operations performed.
*/


// Implement class for minStack.
class minStack {
    vector<pair<int, int>> mnStack;

public:
    // Constructor
    minStack() { }

    // Function to add another element equal to num at the top of stack.
    void push(int num)
    {
        if (mnStack.empty())
            mnStack.push_back({ num, num });
        else
            mnStack.push_back({ num, min(mnStack.back().second, num) });
    }

    // Function to remove the top element of the stack.
    int pop()
    {
        if (mnStack.empty())
            return -1;
        int topNum = mnStack.back().first;
        mnStack.pop_back();
        return topNum;
    }

    // Function to return the top element of stack if it is present. Otherwise return -1.
    int top()
    {
        if (mnStack.empty())
            return -1;
        else
            return mnStack.back().first;
    }

    // Function to return minimum element of stack if it is present. Otherwise return -1.
    int getMin()
    {
        if (mnStack.empty())
            return -1;
        else
            return mnStack.back().second;
    }
};


```