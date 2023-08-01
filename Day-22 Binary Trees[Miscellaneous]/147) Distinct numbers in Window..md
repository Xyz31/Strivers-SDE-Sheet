# Distinct numbers in Window.


# Approach - I Brute force approach
```cpp

/*
    Time complexity: O((N - K) * (K ^ 2))
    Space complexity: O(1)

    Where N denotes the number of elements in the array, and K denotes the size of the window.
*/

vector<int> countDistinctElements(vector<int> &arr, int k) 
{
    int n = arr.size();

    // Create an array to store the number of distinct elements in all windows
    vector<int> answer(n - k + 1);

    // Traverse through each window
    for (int windowNumber = 0; windowNumber <= n - k; windowNumber++) 
    {
        // The variable count store the number of distinct elements in the current window
        int count = 0;

        // Traverse through the elements present in the current window
        for (int index = windowNumber; index <= windowNumber + k - 1; index++) 
        {
            // The variable distinctElement will store if the current element is distinct in the current window or not
            bool distinctElement = true;

            for (int pos = windowNumber; pos <= index - 1; pos++) 
            {
                // Check if ARR[index] is equal to ARR[pos]
                if (arr[index] == arr[pos]) 
                {
                    distinctElement = false;
                    break;
                }
            }

            // Check if distinctElement is true
            if (distinctElement == true) 
            {
                count += 1;
            }
        }

        // Insert count in the array answer
        answer[windowNumber] = count;
    }

    // Return the array answer
    return answer;
}


```

# Approach - II HashMap
```cpp

/*
    Time complexity: O((N - K) * K)
    Space complexity: O(K)

    Where N denotes the number of elements in the array, and K denotes the size of the window.
*/

#include<unordered_map>

vector<int> countDistinctElements(vector<int> &arr, int k) 
{
    int n = arr.size();

    // Create an array to store the number of distinct elements in all windows
    vector<int> answer(n - k + 1);

    // Traverse through each window
    for (int windowNumber = 0; windowNumber <= n - k; windowNumber++) 
    {
        // Maintain a HashMap to store distinct elements in the current window
        unordered_map<int,bool> hashMap;

        for (int index = windowNumber; index < windowNumber + k; index++) 
        {
            // Check if ARR[index] is not present in the HashMap
            if (hashMap.find(arr[index]) == hashMap.end()) 
            {
                hashMap[arr[index]] = true;
            }
        }

        // Insert count in the array answer
        int count = hashMap.size();
        answer[windowNumber] = count;
    }

    // Return the array answer
    return answer;
}


```


# Approach - III Sliding Window
```cpp

/*
    Time complexity: O(N)
    Space complexity: O(K)

    Where N denotes the number of elements in the array, and K denotes the size of the window.
*/

#include<unordered_map>

vector<int> countDistinctElements(vector<int> &arr, int k) 
{
    int n = arr.size();

    // Create an array to store the number of distinct elements in all windows
    vector <int> answer(n - k + 1);

    // Maintain a HashMap to store the frequency of elements in the current window
    unordered_map<int,int> hashMap;

    // Add the frequency of first K element in the HashMap
    for (int i = 0; i < k; i++) 
    {
        hashMap[arr[i]] = hashMap[arr[i]] + 1;
    }

    // Insert the number of distinct elements present in the first window in the array answer
    answer[0] = hashMap.size();

    //  Iterate through all remaining windows
    for (int index = k; index < n; index++) 
    {
        // Decrement the frequency of element in the HashMap by 1
        int element = arr[index - k];
        hashMap[element] -= 1;

        // Check if the frequency of element in the HashMap is 0
        if (hashMap[element] == 0) 
        {
            hashMap.erase(element);
        }

        // Increment the frequency of ARR[index] in the HashMap by 1
        hashMap[arr[index]] = hashMap[arr[index]] + 1;

        // Insert the number of distinct elements present in the window in the array answer
        int windowNumber = index - k + 1;
        answer[windowNumber] = hashMap.size();
    }

    // Return the array answer
    return answer;
}


```