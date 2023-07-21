# Fractional Knapsack Problem


```cpp

#include <bits/stdc++.h>

// Comparator function to sort items based on their value-to-weight ratio
bool comparator(const pair<int, int>& item1, const pair<int, int>& item2) {
    double a = (double)item1.second / item1.first;
    double b = (double)item2.second / item2.first;
    return a > b;
}

// Function to find the maximum value of items that can be carried within a given weight limit
double maximumValue(vector<pair<int, int>>& items, int n, int w) {
    double ans = 0;

    // Sort items in decreasing order of their value-to-weight ratio
    sort(items.begin(), items.end(), comparator);

    int wfilled = 0;
    for (int i = 0; i < n; i++) {
        if (items[i].first + wfilled <= w) {
            // Add the entire item to the knapsack
            ans += items[i].second;
            wfilled += items[i].first;
        } else {
            // Add a fraction of the item to fill the remaining capacity of the knapsack
            int rem = w - wfilled;
            ans += ((double)items[i].second / items[i].first) * (double)rem;
            break;
        }
    }

    return ans;
}

```