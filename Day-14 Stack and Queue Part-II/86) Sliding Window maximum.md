# Sliding Window maximum

```md



```

# Approach -I
```cpp

/*
    Time Complexity = O(N*K)
    Space Complexity = O(N)

    Where N is the number of elements in the given array/list and K is the given window size.
*/

vector<int> slidingWindowMaximum(vector<int> &nums, int &k)
{

    int n = nums.size();

    vector<int> result;

    for (int i = 0; i <= n - k; i++)
    {
        //    Intially assigned to the first value of the window.
        int maxValue = nums[i];

        //    For the whole window we try to find out the maximum value among the array/list elements.
        for (int j = 1; j < k; j++)
        {
            if (nums[i + j] > maxValue)
            {
                maxValue = nums[i + j];
            }
        }

        //    Add maximum of the current window to the result.
        result.push_back(maxValue);
    }

    return result;
}

```

# Approach -II
```cpp

/*
    Time Complexity = O(N* log(K))
    Space Complexity = O(N)
    
    Where N is the number of elements in the given array/list and K is the given window size.
*/

#include <map>

vector<int> slidingWindowMaximum(vector<int> &nums, int &k)
{
    int n = nums.size();

    //    An ordered map to store the frequence of elements in the window.
    map<int, int> window;

    //    Initialise the window with first 'k' - 1 elements.
    for (int i = 0; i < k - 1; i++)
    {
        window[nums[i]]++;
    }

    //    Initialise a vector to store the maximum element of subarrays.
    vector<int> windowMax(n - k + 1, 0);

    //    Start traversing the array.
    for (int high = k - 1; high < n; high++)
    {
        //    Insert the current element in the window.
        window[nums[high]] = window[nums[high]] + 1;

        //    Get the maximum of the current window i.e. maximum of subarray [high-k+1, high].
        windowMax[high - k + 1] = (window.rbegin())->first;

        //    Remove the element at "high" - K + 1 from the window.
        if (window[nums[high - k + 1]] == 1)
        {
            //    Remove the element from the window.
            window.erase(nums[high - k + 1]);
        }
        else
        {
            //    Decrement the frequency by 1.
            window[nums[high - k + 1]]--;
        }
    }

    return windowMax;
}

```

# Approach -III
```cpp

#include <bits/stdc++.h> 
#include <vector>
#include <deque>

/*
    Time Complexity = O(N)
    Space Complexity = O(N)

    Where N is the number of elements in the given array/list.
*/

// Function to find the maximum element in each sliding window of size 'k'
vector<int> slidingWindowMaximum(vector<int> &nums, int &k) {
    int n = nums.size(); // Get the size of the input vector
    vector<int> windowMax; // Vector to store the maximum elements in each window
    deque<int> dq; // Deque to store the indices of elements in decreasing order of their values
    
    for (int i = 0; i < n; i++) {
        // Remove numbers from the front of the deque which are out of the window range of 'k'
        while (!dq.empty() && dq.front() < i - (k - 1))
            dq.pop_front();
        
        // Remove smaller numbers in the current window range as they are not useful
        while (!dq.empty() && nums[dq.back()] < nums[i])
            dq.pop_back();
        
        dq.push_back(i); // Push the current index to the deque
        
        // If the current index is greater than or equal to the first 'k' elements,
        // store the maximum element in the window (front of the deque) to the result vector
        if (i >= k - 1)
            windowMax.push_back(nums[dq.front()]);
    }
    
    return windowMax; // Return the vector containing maximum elements in each sliding window
}


```