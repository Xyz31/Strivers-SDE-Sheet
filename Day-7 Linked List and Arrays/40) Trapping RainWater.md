# Trapping RainWater

Sample Input 1:
4
2 1 1 4

Sample Output 1:
2

Explanation Of Sample Input 1:
Water trapped by:
     block of height 2 is 0 units.
     block of height 1 is 1 unit.
     block of height 1 is 3 1 unit. 
     block of height 4 is 3 0 units.

Hence the total is 2.

## code

```cpp

#include <bits/stdc++.h> 

// Function to calculate the amount of trapped water
long getTrappedWater(long *arr, int n){
    int l = 0, r = n-1;  
    // Pointers for the left and right ends of the array
    long leftMax = 0, rightMax = 0;  
    // Variables to track the maximum height from the left and right sides
    long res = 0;  
    // Variable to store the result (total trapped water)

    while(l <= r){  
        // Iterate until the left and right pointers meet
        if(arr[l] <= arr[r]){  
            // If the height at the left pointer is less than or equal to the height at the right pointer
            if(arr[l] >= leftMax){  
                // If the current height is greater than the maximum height from the left side so far
                leftMax = arr[l];  
                // Update the maximum height from the left side
            } else{
                res += leftMax - arr[l];  
                // Calculate the trapped water by subtracting the current height from the maximum height from the left side
            }
            l++;  
            // Move the left pointer towards the right
        } else{  
            // If the height at the right pointer is greater than the height at the left pointer
            if(arr[r] >= rightMax){  
                // If the current height is greater than the maximum height from the right side so far
                rightMax = arr[r];  
                // Update the maximum height from the right side
            } else{
                res += rightMax - arr[r];  
                // Calculate the trapped water by subtracting the current height from the maximum height from the right side
            }
            r--;  
            // Move the right pointer towards the left
        }
    }

    return res;  
    // Return the total trapped water
}





```