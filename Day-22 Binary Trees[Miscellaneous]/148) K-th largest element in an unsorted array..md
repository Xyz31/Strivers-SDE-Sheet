# K-th largest element in an unsorted array.


# Approach - I Brute force approach
```cpp

/*
	Time Complexity: O(N * log(N))
	Space Complexity: O(1)

	where 'N' is the size of the array.
*/

int kthLargest(vector<int>& arr, int size, int K)
{
	sort(arr.begin(), arr.end(), greater<int>());
	return arr[K - 1];
}

```

# Approach - II Priority Queue(Min-Heap)
```cpp

/*
    Time Complexity: O(K + (N-K) * log(K))
    Space Complexity: O(K)

    where 'N' is the length of the array and 'K' is order of the largest element to be found.
*/

int kthLargest(vector<int>& arr, int size, int K)
{
    // Initializing Priority queue with priority to the min element( functions as Min-Heap).
    priority_queue<int, vector<int>, greater<int> >pq;
    int val;
    for (int i = 0; i < size; i++)
    {
        if (i < K)
        {
            pq.push(arr[i]);
        }

        else
        {
            val = pq.top();
            if (val < arr[i])
            {
                pq.pop();
                pq.push(arr[i]);
            }

        }

    }

    return pq.top();
}

```