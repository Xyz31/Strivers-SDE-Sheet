# K Max Sum Combinations


```cpp


/*
-   To reduce complexity we can reduce number of push operations.
-   If our heap has smaller size than k then push sum in heap.
-   else if sum of element is greater than top element of heap then pop top element and push new sum.
-   Here we are using min heap so top element will be smallest element always.
*/

#include <bits/stdc++.h> 
vector<int> kMaxSumCombination(vector<int> &a, vector<int> &b, int n, int k){
	// Write your code here.

	priority_queue<int, vector<int>, greater<int>> pq;
    for (auto x : a) {
        for (auto y : b) {
            if (pq.size() < k)
                pq.push(x + y);
            else if (x + y > pq.top()) {
                pq.pop();
                pq.push(x + y);
            }
        }
    }
    vector<int> ans(k, 0);
    for (int i = k - 1; i >= 0; i--) {
        ans[i] = pq.top();
        pq.pop();
    }
    return ans;
}


```