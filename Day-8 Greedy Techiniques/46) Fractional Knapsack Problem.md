# Fractional Knapsack Problem



Sample Input 1:
1
6 200
50 40 90 120 10 200 
40 50 25 100 30 45


Sample Output 1:
204.00


Explanation Of Sample Output 1:
The most optimal way to fill the knapsack is to choose full items with weight 10 and value 30, weight 40 and value 50, weight 120 and value 100. Then take weight 30 from the item with weight 50 and value 40.

The total value =  30 + 50 + 100 + (30/50)*(40) = 204.00

```md



```

## code
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