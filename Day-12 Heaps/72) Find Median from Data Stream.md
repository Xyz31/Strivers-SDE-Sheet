# Find Median from Data Stream

```md

Sample Input 1 :
6
6 2 1 3 7 5


Sample Output 1 :
6 4 2 2 3 4


Explanation Of Sample Output 1 :
S = {6}, median = 6
S = {6, 2} -> {2, 6}, median = 4
S = {6, 2, 1} -> {1, 2, 6}, median = 2
S = {6, 2, 1, 3} -> {1, 2, 3, 6}, median = 2
S = {6, 2, 1, 3, 7} -> {1, 2, 3, 6, 7}, median = 3
S = {6, 2, 1, 3, 7, 5} -> {1, 2, 3, 5, 6, 7}, median = 4

```

## code
```cpp

#include <queue>
#include <iostream>
#include <iomanip>



using namespace std;

/*
The time complexity of this code is O(n * log(n))
The space complexity is O(n) since the heaps can store up to n/2 elements at any given time.

*/

void findMedian(int *arr, int n) {
    // Write your code here
    
    priority_queue<int> maxHeap; 
    // Max-heap to store the smaller half of the integers
    priority_queue<int, vector<int>, greater<int>> minHeap; 
    // Min-heap to store the larger half of the integers

    for (int i = 0; i < n; i++) {
        if (maxHeap.empty() || arr[i] < maxHeap.top()) {
            maxHeap.push(arr[i]); 
            // If the current element is smaller than the top of the max-heap, insert it into the max-heap
        } else {
            minHeap.push(arr[i]); 
            // Otherwise, insert it into the min-heap
        }

        // Balance the heaps to maintain the property that the sizes differ by at most one
        if (maxHeap.size() > minHeap.size() + 1) {
            minHeap.push(maxHeap.top()); 
            // Move the top element of the max-heap to the min-heap
            maxHeap.pop();
        } else if (minHeap.size() > maxHeap.size()) {
            maxHeap.push(minHeap.top()); 
            // Move the top element of the min-heap to the max-heap
            minHeap.pop();
        }

        // Calculate the median
        int median;
        if (maxHeap.size() > minHeap.size()) {
            median = maxHeap.top(); 
            // If the max-heap has more elements, the median is the top element of the max-heap
        } else {
            median = (maxHeap.top() + minHeap.top()) / 2; 
            // If the heaps have equal sizes, the median is the average of the top elements of both heaps
        }

        cout << median << " "; 
        // Print the integer part of the median
    }
}

```