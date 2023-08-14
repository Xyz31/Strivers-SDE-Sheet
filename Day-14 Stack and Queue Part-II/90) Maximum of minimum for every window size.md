# Maximum of minimum for every window size

```md



```

# Approach -I
```cpp

/*
    Time Complexity: O(N ^ 3)
    Space complexity: O(1)

    Where 'N' is the number elements present in the given array.
 */

vector<int> maxMinWindow(vector<int> arr, int n) 
{
    // Definition: answer[i] will store the maximum of minimum of every window of size 'i'.
    vector<int> answer(n);
    
	for (int i = 0; i < n; ++i) 
	{
        answer[i] = INT_MIN;
    }

    // Sliding on all possible windows
    for (int i = 0; i < n; ++i) 
	{
        for (int j = i; j < n; ++j) 
		{

            // Start is the starting index of current window
            int start = i;

            //  End is the ending index of current window
            int end = j;

            // Temp will store minimum element for the current window
            int temp = INT_MAX;
            for (int k = start; k <= end; ++k) 
			{
                temp = min(temp, arr[k]);
            }
            
			int length = end - start;

            // Update the answer of current window length
            answer[length] = max(answer[length], temp);
        }
    }

    return answer;
}


```

# Approach - II
```cpp

#include <bits/stdc++.h> 
 

/*
T -O(N)
S-O(2N)
*/

#include <bits/stdc++.h> 
using namespace std;

// Function to calculate the previous smaller element for each element in the array
void prevSmallerFun(vector<int>& nums, vector<int>& res) {
    int n = nums.size();
    stack<int> st;
    
    // Iterate through each element in the array
    for (int i = 0; i < n; i++) {
        // Pop elements from the stack that are greater than or equal to the current element
        while (!st.empty() && nums[st.top()] >= nums[i]) {
            st.pop();
        }
        
        // If the stack becomes empty, there is no previous smaller element
        // Otherwise, the previous smaller element is the top element of the stack
        res[i] = st.empty() ? -1 : st.top();
        
        // Push the current element's index onto the stack
        st.push(i);
    }
}

// Function to calculate the next smaller element for each element in the array
void nextSmallerFun(vector<int>& nums, vector<int>& res) {
    int n = nums.size();
    stack<int> st;
    
    // Iterate through each element in the array in reverse order
    for (int i = n - 1; i >= 0; i--) {
        // Pop elements from the stack that are greater than or equal to the current element
        while (!st.empty() && nums[st.top()] >= nums[i]) {
            st.pop();
        }
        
        // If the stack becomes empty, there is no next smaller element
        // Otherwise, the next smaller element is the top element of the stack
        res[i] = st.empty() ? n : st.top();
        
        // Push the current element's index onto the stack
        st.push(i);
    }
}

// Function to find the maximum element in each window of size 'n'
vector<int> maxMinWindow(vector<int> a, int n) {
    int len = a.size();
    vector<int> res(len, INT_MIN); // Initialize result vector with minimum values
    vector<int> nextSmaller(len, -1), prevSmaller(len, len);
    
    // Calculate the next smaller and previous smaller elements
    nextSmallerFun(a, nextSmaller);
    prevSmallerFun(a, prevSmaller);
    
    // Iterate through each element in the array
    for (int i = 0; i < len; i++) {
        // Calculate the length of the window
        int windowLen = nextSmaller[i] - prevSmaller[i] - 1;
        
        // Update the maximum element in the window
        res[windowLen - 1] = max(res[windowLen - 1], a[i]);
    }
    
    // Update the maximum element for remaining windows
    for (int i = len - 2; i >= 0; i--) {
        res[i] = max(res[i], res[i + 1]);
    }
    
    return res;
}


```