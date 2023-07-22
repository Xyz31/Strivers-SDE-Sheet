# N meetings in one room


```cpp

#include <bits/stdc++.h>

struct meeting {
    int start;
    int end;
    int pos;
};

bool comparator(struct meeting m1, meeting m2) {
    // The comparator function is used to sort the meetings based on their end times.
    // If m1's end time is earlier than m2's end time, m1 should come before m2.
    if (m1.end < m2.end) return true;
    // If m1's end time is later than m2's end time, m1 should come after m2.
    if (m1.end > m2.end) return false;
    // If the end times are the same, we prioritize the meeting with a smaller position number.
    if (m1.pos > m2.pos) return false;
    return true;
}

vector<int> maximumMeetings(vector<int>& start, vector<int>& end) {
    // Write your code here.

    int n = start.size();
    struct meeting meet[n];

    // Fill the meeting structure with the start, end, and position data.
    for (int i = 0; i < start.size(); i++) {
        meet[i].start = start[i];
        meet[i].end = end[i];
        meet[i].pos = i + 1;
    }

    // Sort the meetings based on the defined comparator function.
    sort(meet, meet + n, comparator);

    vector<int> ans;
    ans.push_back(meet[0].pos);
    int limit = meet[0].end;

    // Iterate over the sorted meetings and select the maximum number of non-overlapping meetings.
    for (int i = 1; i < start.size(); i++) {
        if (limit < meet[i].start) {
            limit = meet[i].end;
            ans.push_back(meet[i].pos);
        }
    }

    return ans;
}


```