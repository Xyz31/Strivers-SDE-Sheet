# Maximum activities

```cpp

/*
 finding the maximum number of activities that can be scheduled without overlapping, 
 given their start and finish times. 
*/

#include <bits/stdc++.h>

// Comparator function used to sort activities based on their finish times in ascending order
bool comparator(const pair<int ,int> &a, const pair<int ,int> &b){
    return a.second < b.second;
}

// Function to find the maximum number of activities that can be scheduled without overlapping
int maximumActivities(vector<int>& start, vector<int>& finish) {
    int ans = 0;
    int n = start.size();
    vector<pair<int, int>> meet;

    // Create a vector of pairs where each pair represents an activity with its start and finish times
    for (int i = 0; i < n; i++) {
        meet.push_back(make_pair(start[i], finish[i]));
    }

    // Sort the activities based on their finish times using the comparator function
    sort(meet.begin(), meet.end(), comparator);

    int temp = meet[0].second;
    ans++;

    // Iterate through the sorted activities and count the number of activities that can be scheduled without overlapping
    for (int i = 1; i < n; i++) {
        if (temp <= meet[i].first) {
            ans++;
            temp = meet[i].second;
        }
    }

    return ans;
}

```