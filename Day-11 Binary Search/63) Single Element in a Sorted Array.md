# Single Element in a Sorted Array


```cpp

int singleNonDuplicate(vector<int>& nums)
{
	// Write your code here
	// if the single element is at the last position
        int start = 0, end = nums.size() - 2;
        while(start <= end) {
            int mid = start + (end - start) / 2;
            // left part so move to the right
            if(nums[mid] == nums[mid ^ 1])
                start = mid + 1;
            else
                end = mid - 1;
        }
        return nums[start];
}

```