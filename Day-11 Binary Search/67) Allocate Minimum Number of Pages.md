# Aggressive Cows


```cpp

#include <bits/stdc++.h>

// Function to check if it's feasible to complete the test in 'maxTime' time per day
bool isFeasible(long long maxTime, int n, std::vector<int>& time) {
    int days = 1;                 // Number of days to complete the test, initialized to 1
    long long currTime = 0;       // Current time spent on the test, initialized to 0

    // Iterate through the time required for each problem in the vector 'time'
    for (int i = 0; i < time.size(); i++) {
        if (time[i] > maxTime) {
            return false;         // If time required for a problem exceeds 'maxTime', it's not feasible
        } else if (currTime + time[i] <= maxTime) {
            currTime += time[i];  // If the problem can be solved within 'maxTime', add it to the current day
        } else {
            days++;               // Otherwise, start a new day to solve the problem
            currTime = time[i];   // Set the current day's time to the time required for the current problem
        }
    }
    return days <= n;            // Check if the number of days needed to complete the test is less than or equal to 'n'
}

// Function to find the minimum time required for Ayush to give the ninja test
long long ayushGivesNinjatest(int n, int m, std::vector<int>& time) {
    long long left = *max_element(time.begin(),time.end());               // Initialize the left boundary of the binary search range to 1
    long long right = std::accumulate(time.begin(), time.end(), 0LL);  // Calculate the sum of all times as the right boundary
    long long result = LLONG_MAX;     // Initialize 'result' to the maximum possible value of long long

    // Binary search to find the minimum feasible time to complete the test
    while (left <= right) {
        long long mid = left + (right - left) / 2;  // Calculate the middle value of the current search range

        // Check if 'mid' time is feasible to complete the test
        if (isFeasible(mid, n, time)) {
            result = std::min(result, mid);       // Update 'result' with the minimum feasible time found so far
            right = mid - 1;                      // Continue searching in the left half of the current range
        } else {
            left = mid + 1;                       // Continue searching in the right half of the current range
        }
    }
    return result;                               // Return the minimum feasible time to complete the test
}


```