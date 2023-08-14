# Next Greater Element

```md



```

```cpp

#include <bits/stdc++.h> 

/*
    Time Complexity : O(N)
    Space Complexity : O(N)
    
    Where N is the length of the array.
*/

// Function to find the next greater element for each element in the array
vector<int> nextGreater(vector<int> &arr, int n) {
    // Write your code here

    
    
    vector<int> ans(n, -1); // Initialize a vector to store the next greater elements, initially set to -1
    stack<int> st; // Create a stack to store the indices of the array elements

    for (int i = n - 1; i >= 0; i--) // Traverse the array in reverse order
    {
        while (!st.empty() && st.top() <= arr[i])
            st.pop(); // Pop elements from the stack until a greater element is found or the stack becomes empty
        
        if (!st.empty())
            ans[i] = st.top(); // If a greater element is found, store it in the ans vector
        
        st.push(arr[i]); // Push the current element into the stack
    }

    return ans; // Return the vector containing the next greater elements

}

```