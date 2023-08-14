# Next Smaller Element

```md



```


```cpp

/*
    Time Complexity: O(N)
    Space Complexity: O(N)

    Where N denotes the number of elements in the array.
*/

#include <stack>

vector<int> nextSmallerElement(vector<int>& arr, int n) 
{
    // Defining the vector to store next smaller elements for the array. 
    vector<int> ans(n);

    // Defining the stack and pushing -1 to it.
    stack < int > stk;
    stk.push(-1);

    // Iterating through all the array elements from backwards.
    for (int i = n - 1; i >= 0; i--)
    {
        // Removing all the elements greater than or equal to current element from the stack.
        while (stk.top() >= arr[i])
        {
            stk.pop();
        }

        // Setting the next smaller element as the element at top of stack.
        ans[i] = stk.top();

        // Pushing the current element into the stack.
        stk.push(arr[i]);
    }

    // Returning the final vector after all the iterations.
    return ans;
}

```