# Reverse Pairs

## code 

```cpp

#include <bits/stdc++.h> 

// This function merges two sorted subarrays and counts the reverse pairs.
void merge(vector<int>& nums, int low, int mid, int high, int& reversePairsCount){
    int j = mid+1;
    for(int i=low; i<=mid; i++){
        while(j<=high && nums[i] > 2*(long long)nums[j]){
            j++;
        }
        reversePairsCount += j-(mid+1);
    }
    
    int size = high-low+1;
    vector<int> temp(size, 0);
    int left = low, right = mid+1, k=0;
    
    // Merge the two sorted subarrays into a temporary array.
    while(left<=mid && right<=high){
        if(nums[left] < nums[right]){
            temp[k++] = nums[left++];
        }
        else{
            temp[k++] = nums[right++];
        }
    }
    
    // Copy any remaining elements from the left subarray.
    while(left<=mid){
        temp[k++] = nums[left++]; 
    }
    
    // Copy any remaining elements from the right subarray.
    while(right<=high){
        temp[k++] = nums[right++]; 
    }
    
    // Copy the sorted elements from the temporary array back to the original array.
    int m=0;
    for(int i=low; i<=high; i++){
        nums[i] = temp[m++];
    }
}

// This function performs the merge sort algorithm.
void mergeSort(vector<int>& nums, int low, int high, int& reversePairsCount){
    if(low >= high){
        return;
    }
    
    // Divide the array into two halves and recursively sort them.
    int mid = (low + high) >> 1;
    mergeSort(nums, low, mid, reversePairsCount);
    mergeSort(nums, mid+1, high, reversePairsCount);
    
    // Merge the sorted halves.
    merge(nums, low, mid, high, reversePairsCount);
}

// This function calculates the number of reverse pairs in the array.
int reversePairs(vector<int> &arr, int n){
    int reversePairsCount = 0;
    
    // Call the mergeSort() function to perform sorting and count reverse pairs.
    mergeSort(arr, 0, arr.size()-1, reversePairsCount);
    
    return reversePairsCount;
}


```