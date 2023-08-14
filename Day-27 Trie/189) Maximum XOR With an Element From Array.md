# Maximum XOR With an Element From Array


```md



```
 
```cpp

/*
    Function to find the maximum XOR value of each query element with any array element 
    that is less than or equal to it.

    Time Complexity : O(N*M)
    Space Complexity : O(1)

    Where 'N' is the size of 'arr', and 'M' is the number of queries.
*/

vector<int> maxXorQueries(vector<int> &arr, vector<vector<int>> &queries) {
    // Size of the array and number of queries.
    int n = arr.size();
    int m = queries.size();

    // Create a result vector initialized with -1 to store the answer of each query.
    vector<int> result(m, -1);

    // Finding the answer for each query.
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            // If the array element is less than or equal to the query's upper bound (queries[i][1]),
            // calculate the XOR value with the query's XOR value (queries[i][0]) and update the result.
            if (arr[j] <= queries[i][1]) {
                result[i] = max(result[i], arr[j] ^ queries[i][0]);
            }
        }
    }

    return result; // Return the vector containing the maximum XOR values for each query.
}


/*
    Time Complexity : O(N*(log(N)) + M*(log(M)))
    Space Complexity : O(N + M)

    Where 'N' is the size of ‘ARR’, and ‘M’  is the number of queries.
*/

#include <algorithm>

struct TrieNode {
    TrieNode *children[2];
};

void insert(TrieNode *root, int num) {
    TrieNode *ptr = root;

    for(int i = 30; i >= 0; i--) {
        if(num & (1 << i)) {
            if(ptr->children[1] == NULL) {
                ptr->children[1] = new TrieNode();
            }
            ptr = ptr->children[1];
        }
        else {
            if(ptr->children[0] == NULL) {
                ptr->children[0] = new TrieNode();
            }
            ptr = ptr->children[0];
        }
    }
}

vector<int> maxXorQueries(vector<int>& arr, vector<vector<int>>& queries)
{

    //  Size of array and number of queries.
    int n = arr.size();
    int m = queries.size();

    vector<int> result(m, -1), order(m);

    //  Sort ‘arr’ in non-decreasing order.
    sort(arr.begin(), arr.end());

    for(int i = 0; i < m; i++)
    {
        order[i] = i;
    }

    //  Order in which queries will be processed.
    sort(order.begin(), order.end(), [&](int i, int j) -> bool {
        return queries[i][1] < queries[j][1];
    });

    TrieNode *root = new TrieNode();
    int p = 0;

    //  Finding answer of each query.
    for(int i = 0; i < m; i++)
    {

        //  Index of query process in current iteration.
        int id = order[i];

        //  Insert integers of 'arr' smaller or equal to queries[id][1] in trie.
        while(p < n && arr[p] <= queries[id][1])
        {
            insert(root, arr[p]);
            p++;
        }

        //  If trie is empty then answer to this query is -1.
        if(root->children[0] == NULL && root->children[1] == NULL)
        {
            continue;
        }

        TrieNode *ptr = root;
        int ans = 0;

        for(int j = 30; j >= 0; j--)
        {

            // If jth bit is set in query[id][0].
            if(queries[id][0] & (1 << j))
            {
                if(ptr->children[0] != NULL)
                {
                    ptr = ptr->children[0];
                    ans = ans | (1 << j);
                }
                else
                {
                    ptr = ptr->children[1];
                }

            }
            else
            {

                // If jth bit is not set in query[id][0].
                if(ptr->children[1] != NULL) {
                    ptr = ptr->children[1];
                    ans = ans | (1 << j);
                } else {
                    ptr = ptr -> children[0];
                }
            }
        }

        result[id] = ans;

    }

    return result;
}


```