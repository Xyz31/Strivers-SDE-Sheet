# Job Sequencing Problem

```cpp

#include <bits/stdc++.h>

using namespace std;


// Comparator function to sort jobs based on their deadlines in ascending order
bool compareJobs(const std::vector<int>& job1, const std::vector<int>& job2) {
    return job1[0] < job2[0]; // Sort based on deadline
}



int jobScheduling(std::vector<std::vector<int>>& jobs) {
    // Sort jobs based on deadlines in ascending order
    
    // Custom comparator function to sort jobs based on deadlines in ascending order
    /*
    std::sort(jobs.begin(), jobs.end(), [](const std::vector<int>& job1, const std::vector<int>& job2) {
        return job1[0] < job2[0];
    });
    */
    sort(jobs.begin(), jobs.end(), compareJobs); // Sort jobs using the compareJobs comparator function
    
    std::priority_queue<int, std::vector<int>, std::greater<int>> profitQueue;
    
    int maxProfit = 0;
    
    // Iterate through the sorted jobs
    for (const std::vector<int>& job : jobs) {
        int deadline = job[0];
        int profit = job[1];
        
        // Check if the job's deadline allows it to be scheduled within the available time slots
        if (deadline > profitQueue.size()) {
            profitQueue.push(profit); 
            // Add the job's profit to the priority queue
        }
        else if (!profitQueue.empty() && profit > profitQueue.top()) {
            profitQueue.pop(); 
            // Remove the job with the lowest profit so far
            profitQueue.push(profit); 
            // Add the current job's profit to the priority queue
        }
    }
    
    // Sum up the profits from the priority queue
    while (!profitQueue.empty()) {
        maxProfit += profitQueue.top();
        profitQueue.pop();
    }
    
    // Return the maximum profit that can be made
    return maxProfit;
}

```