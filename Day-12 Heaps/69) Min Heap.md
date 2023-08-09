# Min Heap

```md
Sample Input 1 :
2
3
0 2
0 1
1
2
0 1
1


Sample Output 1 :
1
1


Explanation Of Sample Input 1 :
For the first test case:-
Insert 2 in the heap and currently, 2 is the smallest element in the heap.
Insert 1 in the heap and now the smallest element is 1.
Return and remove the smallest element which is 1.

For the second test case:-
Insert 1 in the heap and currently, 1 is the smallest element in the heap.
Return the smallest element from the heap which is 1 and remove it.

```

## code
```cpp

#include <bits/stdc++.h>


vector<int> minHeap(int n, vector<vector<int>>& q) {
    vector<int> result; 
    // Vector to store the popped elements from the min heap
    priority_queue<int, vector<int>, greater<int>> pq; // Min heap implemented using priority_queue

    for (int i = 0; i < n; i++) {
        int type = q[i][0]; 
        // Extracting the query type

        if (type == 0) { 
            // If the query type is 0, insert the number into the min heap
            int num = q[i][1]; 
            // Extracting the number to be inserted
            pq.push(num); 
            // Inserting the number into the min heap
        } else if (type == 1) { 
            // If the query type is 1, pop the top element from the min heap
            if (!pq.empty()) { 
                // Checking if the min heap is not empty
                result.push_back(pq.top()); 
                // Adding the top element to the result vector
                pq.pop(); 
                // Removing the top element from the min heap
            }
        }
    }

    return result; 
    // Returning the vector containing the popped elements from the min heap
}


```