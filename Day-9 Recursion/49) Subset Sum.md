# Subset Sum

Sample Input 1 :
3
1 2 3


Sample Output 1 :
0 1 2 3 3 4 5 6


Explanation For Sample Output 1:
For the first test case,
Following are the subset sums:
0 (by considering empty subset)
1
2
1+2 = 3
3
1+3 = 4
2+3 = 5
1+2+3 = 6
So, subset-sums are [0,1,2,3,3,4,5,6]

## code
```cpp

/*
 * This code implements a function subsetSum() that finds all possible subset sums of a given vector of integers.
 * The solve() function is a helper function used recursively to generate the subsets and calculate their sums.
 */

void solve(vector<int>& ans, vector<int>& temp, vector<int>& num, int n) {
	// Base case: If n is less than 0, we have considered all elements in num
	if (n < 0) {
		int k = accumulate(temp.begin(), temp.end(), 0);  
		// Calculate the sum of elements in temp
		ans.push_back(k);  
		// Add the sum to the ans vector
		return;
	}

	solve(ans, temp, num, n - 1); 
	// Recursive call without including the current element
	temp.push_back(num[n]);  
	// Include the current element in the subset
	solve(ans, temp, num, n - 1);  
	// Recursive call including the current element
	temp.pop_back();  
	// Remove the current element from the subset
	return;
}

vector<int> subsetSum(vector<int>& num) {
	// The subsetSum function generates all subset sums of the given vector num

	vector<int> ans;  
	// Vector to store the subset sums
	vector<int> temp;  
	// Temporary vector to store the subsets
	solve(ans, temp, num, num.size() - 1);  
	// Call the solve function to generate subsets and their sums
	sort(ans.begin(), ans.end());  
	// Sort the subset sums in ascending order
	return ans;  
	// Return the vector of subset sums
}




```