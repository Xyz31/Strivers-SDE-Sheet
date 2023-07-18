# Grid Unique Paths

## code 

```cpp

#include <bits/stdc++.h> 

int uniquePaths(int m, int n) {
	// Calculate the number of unique paths from (0,0) to (m-1,n-1) in a grid of size m x n.
	// The grid is represented by m rows and n columns.
	
	double ans = 1; // Variable to store the result
	
	int t = m+n-2; // Total number of steps required to reach the destination
	int r = m-1;   // Number of steps required to move vertically
	
	// Calculate the binomial coefficient using the formula C(t,r) = (t!)/((t-r)! * r!)
	for(int i=1; i<=r; i++){
		ans = ans * (t-r+i)/i; // Multiply ans by (t-r+i)/i to calculate the next term of the binomial coefficient
	}
	
	return (int)ans; // Return the result as an integer
}


```