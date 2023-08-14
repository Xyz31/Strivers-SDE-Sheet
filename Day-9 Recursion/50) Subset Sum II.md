# Subset Sum II

Sample Input 1:
2
3
1 1 3
4
1 3 3 3


Sample Output 1:
1
1 1
1 3
3
1 1 3

1
1 3
1 3 3
1 3 3 3 
3 
3 3
3 3 3


Explanation Of Sample Input 1:
For the first test case,
The unique subsets will be  [ ],[1],[1,1],[1,3],[3],[1,1,3]. 

For the second test case:
The unique subsets will be  [ ],[1,3],[1,3,3],[1,3,3,3],[3],[3,3],[3,3,3]. 

```md



```

## code
```cpp

#include <bits/stdc++.h> 

/*

The function then proceeds to generate subsets by considering two cases:

Pick the element and move to the next index: 
The current element at index ind is added to the temp vector using temp.push_back(arr[ind]). 
Then, the function is recursively called with ind+1 to move to the next index and continue generating subsets.

Not pick the element and move to the next index: 
The most interesting part is here. 
After removing the previously added element from the temp vector using temp.pop_back(), 
the code checks if there are more elements with the same value as the current element. 
It does this by using a while loop: while(ind+1 < arr.size() && arr[ind] == arr[ind+1]) ind++;. 
This loop skips all the consecutive elements with the same value as the current element. 
The purpose of this loop is to avoid generating duplicate subsets that include the same element multiple times. 
After skipping these elements, the function is recursively called with ind+1 to move to the next index and continue generating subsets.

*/

void generateSubset(int ind ,int n, vector<int>& arr, vector<int>& temp, vector<vector<int>>& ans) {
    if (ind == n) {
        ans.push_back(temp);
        return;
    }

    // Pick the element and move to next
    temp.push_back(arr[ind]);
    generateSubset(ind+1,n, arr, temp, ans);
    

    // Not pick the element and move to next
    temp.pop_back();
    //The purpose of this loop is to avoid generating duplicate subsets that include the same element multiple times.
    while(ind+1 < arr.size() && arr[ind] == arr[ind+1])
        ind++;

    generateSubset(ind+1,n, arr, temp, ans);
    
    return;
}

vector<vector<int>> uniqueSubsets(int n, vector<int>& arr) {
    vector<vector<int>> ans;
    vector<int> temp;

    sort(arr.begin(),arr.end());
    generateSubset(0,n, arr, temp, ans);
    sort(ans.begin(),ans.end());
    return ans;
}


```