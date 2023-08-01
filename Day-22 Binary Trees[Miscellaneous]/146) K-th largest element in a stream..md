# K-th largest element in a stream.


# Approach - I Brute Force
```cpp

/*
    Time Complexity : O((N ^ 2) * log(N))
    Space Complexity : O(N)

    Where 'N' is the total number of elements read at runtime.
*/

#include <algorithm>

class Kthlargest {
public:
    int size;
    vector<int> aux;

    Kthlargest(int k, vector<int> &arr) {
        size = k;
        for (auto it : arr) {
            aux.push_back(it);
        }

        // Sort the array in descending order.
        sort(aux.rbegin(), aux.rend());
    }

    int add(int num) {

        // After every addition, again sort the array.
        aux.push_back(num);
        sort(aux.rbegin(), aux.rend());

        // Return the top element.
        return aux[size - 1];
    }

};

```

# Approach - II PriorityQueue
```cpp

/*
      Time Complexity : O(Nlog(K))
      Space Complexity : O(N),

      where N is the maximum number of integers read at runtime and K is the required order of number in sorted order
*/


#include<queue>

class Kthlargest {
public:

    // Initialise priority queue and 'size'.
    int size;
    priority_queue<int, vector<int>, greater<int>> pq;

    // Initialse the 'Kthlargest' object with 'arr'.
    Kthlargest(int k, vector<int> &arr) {
        size = k;
        for (auto it : arr) {
            pq.push(it);
            if (pq.size() > size) {
                pq.pop();
            }
        }
    }

    int add(int num) {

        // Push the current 'num' in priority queue.
        pq.push(num);

        // Maintain only 'k' elelments in priority queue.
        if (pq.size() > size) {
            pq.pop();
        }

        // Return the top element.
        return pq.top();
    }


};

```