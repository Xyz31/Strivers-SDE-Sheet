# K Most Frequent Elements

```md
Sample Input 1:
5 2
1 2 2 3 3 


Sample Output 1:
2 3


Explanation Of Sample Input 1:
The answer will {2, 3} as 2 and 3 are the elements occurring the most number of times.

```


## code
```cpp


#include <bits/stdc++.h> 
using namespace std;

#include <vector>
#include <unordered_map>
#include <queue>

vector<int> KMostFrequent(int n, int k, vector<int>& nums) {
    // Create a dictionary to store frequency counts
    unordered_map<int, int> frequency;

    // Iterate through the array and update frequency counts
    for (int num : nums) {
        frequency[num]++;
    }

    // Create a priority queue (min heap) to store elements based on frequency counts
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    // Iterate through the dictionary and add elements to the priority queue
    for (auto it = frequency.begin(); it != frequency.end(); ++it) {
        pq.push(make_pair(it->second, it->first));
        
        // If the size of the priority queue exceeds 'K', remove the element with the minimum frequency count
        if (pq.size() > k) {
            pq.pop();
        }
    }

    // Create a vector and add elements from the priority queue
    vector<int> result;
    while (!pq.empty()) {
        result.push_back(pq.top().second);
        pq.pop();
    }

    // Reverse the vector to get the elements in any order
    reverse(result.begin(), result.end());

    return result;
}


/*
#include <bits/stdc++.h> 

vector<int> KMostFrequent(int n, int k, vector<int> &nums)
{
    // Write your code here.

}

*/

```