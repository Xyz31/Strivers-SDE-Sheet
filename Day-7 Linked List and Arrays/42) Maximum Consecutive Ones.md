# Maximum Consecutive Ones.md


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