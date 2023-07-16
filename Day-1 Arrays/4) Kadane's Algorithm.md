# Kadane's Algorithm - Maximum Subarray Sum

### code

```cpp

#include <bits/stdc++.h> 
long long maxSubarraySum(int arr[], int n)
{
    /*
        Don't write main().
        Don't read input, it is passed as function argument.    
        No need to print anything.
        Taking input and printing output is handled automatically.
    */
    long long ans=-10e6-1;
    long long windowSum=-10e6-1;

    for(int i=0;i<n;i++){
        windowSum= arr[i] < windowSum+arr[i] ?windowSum+arr[i]:arr[i];
        // windowSum = max(windowSum+arr[i],arr[i]);
        ans=ans<windowSum? windowSum:ans;
    }
    
    return ans>0?ans:0;
}

```