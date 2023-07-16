# Next Permutation

### code

```cpp

#include <bits/stdc++.h> 
vector<int> nextPermutation(vector<int> &permutation, int n)
{
        //  Write your code here.
        vector<int> nums = permutation;
        int s=nums.size();
        if(s<=1) return nums;
        int i=s-2,j=s-1;
        for(;i>=0;i--){
            if(nums[i]<nums[i+1]) break;
        }
        if(i<0) reverse(nums.begin(),nums.end());
        else{
            for(;j>i;j--){
                if(nums[j]>nums[i]) break;
            }
            swap(nums[i],nums[j]);
            reverse(nums.begin()+i+1,nums.end());
        }
        return nums;


}

```