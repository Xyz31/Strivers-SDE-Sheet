# K-th element of two sorted arrays


```cpp

#include<limits.h>

int ninjaAndLadoos(vector<int> &arr1, vector<int> &arr2, int n1, int n2, int k) {
    // Write your code here.
    // we will calculate the contribution size of the smaller array
        if(n1 > n2)
            return ninjaAndLadoos(arr2, arr1, n2, n1, k);
        
        // monotonic search space for binary search
        /*
            edge case: you can't always pick 0 elements from arr1 and n2 elements from arr2
            if k > n2 then u need to pick atleast k - n2 from arr1 since we need to pick k elements overall
        */
        int start = max(0, k - n2), end = min(k, n1);
        
        while(start <= end) {
            // contribution size in each array
            // to compute left half of the final merged array, we need k elements
            int mid1 = start + (end - start) / 2;
            int mid2 = k - mid1;
            
            // 4 variables to check the validity of partition
            // max values in the left part of array
            int max1 = mid1 == 0 ? INT_MIN : arr1[mid1 - 1];
            int max2 = mid2 == 0 ? INT_MIN : arr2[mid2 - 1];
            
            // min values in the right part of array
            int min1 = mid1 == n1 ? INT_MAX : arr1[mid1];
            int min2 = mid2 == n2 ? INT_MAX : arr2[mid2];
            
            // elements on the left part <= elements on the right part for the partition to be valid
            // max1 <= min1 is implied as the array is sorted
            if(max1 <= min2 && max2 <= min1) {
                return max(max1, max2);
            }
            // consider min2 before max1, dont consider max1 for now
            // decrease the contribution size of smaller array
            else if(max1 > min2)
                end = mid1 - 1;
            else
                start = mid1 + 1;
        }
        return -1;
}

```