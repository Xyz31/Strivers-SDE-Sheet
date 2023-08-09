# Median of 2 sorted arrays

```md
Sample Input 1:
3 3
2 4 6
1 3 5

Sample Output 1:
3.5


Explanation Of Sample Input 1 :
The array after merging 'a' and 'b' will be { 1, 2, 3, 4, 5, 6 }. 
Here two medians are 3 and 4. So the median will be the average of 3 and 4, which is 3.5.

```

## code

```cpp

double median(vector<int>& nums1, vector<int>& nums2) {
	// Write your code here.
	int n1 = nums1.size();
        int n2 = nums2.size();
        // we will calculate the contribution size of the smaller vector
        if(n1 > n2)
            return median(nums2, nums1);
        
        // monotonic search space for binary search
        int start = 0, end = n1;
        
        while(start <= end) {
            // contribution size in each array
            // to compute left half of the final merged array, we need (n1 + n2 + 1) / 2 elements.
            int mid1 = start + (end - start) / 2; // contrib size of nums1 = mid elements towards the final merged left half
            int mid2 = (n1 + n2 + 1) / 2 - mid1;
            
            // 4 variables to check the validity of the partition
            // max values in the left part of each vector, handle corner cases            
            int max1 = (mid1 == 0) ? INT_MIN : nums1[mid1 - 1];
            int max2 = (mid2 == 0) ? INT_MIN : nums2[mid2 - 1];
            
            // min values in the right part of each vector, handle corner cases
            int min1 = (mid1 == n1) ? INT_MAX : nums1[mid1];
            int min2 = (mid2 == n2) ? INT_MAX : nums2[mid2];
            
            // elements on left part should be <= elements on the right part, for the partition to be valid
            // max1 <= min1 is impied as the vector is sorted
            if(max1 <= min2 and max2 <= min1) {
                // odd number of elements
                if((n1 + n2) % 2 == 1)
                    return (double)max(max1, max2);
                else 
                    return (double)(min(min1, min2) + max(max1, max2)) / 2;
            }
            // consider min2 first before max1, dont consider max1 for now
            // decrease the contribution size of smaller vector
            else if(max1 > min2)
                end = mid1 - 1;
            else
                start = mid1 + 1;
        }
        return -1;
}

```