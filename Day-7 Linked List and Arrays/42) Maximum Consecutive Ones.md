# Maximum Consecutive Ones.md

Sample Input 1:
1
7
1 0 0 1 1 0 1   
1

Sample Output 1:
4 

Explanation Of Sample Input 1:
Here we can replace at-most one 0 by 1 ( since K = 1 ). So the longest consecutive subarray with all 1’s that we can get is by replacing the 0 present at index 5.    

So the updated array will be {1,0,0,1,1,1,1}.

As we can see in the updated array the longest subarray with all 1’s is from index 3 of length 4.

## code
```cpp

int longestSubSeg(vector<int> &arr , int n, int k){
    // Write your code here.

    int i = 0, j = 0, cnt = 0, len = 0;

    while (j < n) {
        // If the current element is zero, increment the count
        if (arr[j] == 0) {
            cnt++;

            // If the count of zeroes exceeds the maximum allowed (k), move the left pointer and decrease the count
            while (i < j && cnt > k) {
                if (arr[i] == 0) {
                    cnt--;
                }
                i++;
            }
        }

        // Update the maximum length if necessary
        len = max(len, j - i + 1);
        j++;
    }

    return len;
}


```