# Search In Rotated Sorted Array

```md
Sample Input 1:
4
2 5 -3 0
2
5
1


Sample Output 1:
1
-1


Explanation For Sample Input 1:
In the 1st test case, 5 is found at index 1

In the 2nd test case, 1 is not found in the array, hence return -1.

```

## code
```cpp

int search(int* nums, int n, int target) {
    // Write your code here.
    int start = 0, end = n - 1;
        
        while(start <= end) {
            int mid = start + (end - start) / 2;
            
            if(target == nums[mid])
                return mid;
            
            if(nums[mid] >= nums[start]) {
                // part 1 of the array
                // check if target lies in the first part
                if(target >= nums[start] and target < nums[mid])
                    end = mid - 1;
                else
                    start = mid + 1;
            }
            else {
                // part 2 of the array
                if(target > nums[mid] and target <= nums[end])
                    start = mid + 1;
                else
                    end = mid - 1;
            }
        }
        return -1;
}

```