# Merge Overlapping Subintervals

### code

```cpp

#include <bits/stdc++.h> 
/*

    intervals[i][0] = start point of i'th interval
    intervals[i][1] = finish point of i'th interval

*/

vector<vector<int>> mergeIntervals(vector<vector<int>> &intervals)
{
    // Write your code here.
    int n=intervals.size();
    if(n<=1){
        return intervals;
    }

    sort(intervals.begin() , intervals.end());
    vector<int> temp=intervals[0];
    vector<vector<int>> ans;
    for(auto x: intervals){
        if(x[0] <= temp[1]){
            temp[1] = max(temp[1],x[1]);
        }else{
            ans.push_back(temp);
            temp = x;
        }
    }
    ans.push_back(temp);

    return ans;
}


```