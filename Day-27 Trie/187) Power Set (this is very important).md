# Power Set (this is very important)


```md



```
 

```cpp


/*
#include <bits/stdc++.h> 
vector<vector<int>> pwset(vector<int>v)
{
    //Write your code here
}
*/


#include <bits/stdc++.h> 

using namespace std;


/*
    Time Complexity: O(N*(2^N))
    Space Complexity: O(N*(2^N))

    Where N is the number of elements in array
*/

vector<vector<int>> pwset(vector<int> arr) 
{
    int n = arr.size();

    // Create an array to store all subsets
    vector<vector<int>> ans;

    for (int i = 0; i <= pow(2, n); i++)
    {
        vector<int> temp;

        // Traverse through the array ARR
        for (int j = 0; j < n; j++) 
        {
            // Check if j-th bit is set
            if (i & (1 << j)) 
            {
                temp.push_back(arr[j]);
            }
        }

        // Insert the subset temp in ans
        ans.push_back(temp);
    }

    // Return the array ans
    return ans;
}


```