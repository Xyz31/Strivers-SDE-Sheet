# Stock span problem

```md



```

```cpp

#include <bits/stdc++.h>
using namespace std;

// Function to find the spans of stock prices
vector<int> findSpans(vector<int> &price) {
    vector<int> spans(price.size(), 1); // Initialize all spans to 1
    stack<pair<int, int>> st; // Stack to store pairs of price and span

    for (int i = 0; i < price.size(); i++) {
        int currPrice = price[i];
        int currSpan = 1;

        // Pop elements from the stack while the top element's price is less than or equal to the current price
        while (!st.empty() && st.top().first <= currPrice) {
            currSpan += st.top().second; // Calculate the span for the current day
            st.pop(); // Remove the top element as it's no longer needed for further calculations
        }

        // Push the current price and its span into the stack for future calculations
        st.push({ currPrice, currSpan });

        // Save the calculated span for the current day in the spans vector
        spans[i] = currSpan;
    }

    return spans; // Return the vector containing the spans for each day
}


```