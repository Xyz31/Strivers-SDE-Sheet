# Stock Buy and Sell - Best Time to Buy and Sell Stock

### code 

```cpp

#include <bits/stdc++.h> 

//Question no 6
int maximumProfit(vector<int> &prices){
    // Write your code here.

    // stack<int> st;
    int n = prices.size();
    int ans=0,mini=10e9+1;
    for(int i=0;i<n;i++){
        mini = min(mini,prices[i]);
        ans = max(ans,prices[i]-mini);
    }
    return ans;
}

```