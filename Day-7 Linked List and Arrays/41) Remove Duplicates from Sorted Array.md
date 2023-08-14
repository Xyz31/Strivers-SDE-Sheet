# Remove Duplicates from Sorted Array

Sample Input 1:
10
1 2 2 3 3 3 4 4 5 5 

Sample Output 1:
5

Explanation Of Sample Input 1:
The new array will be [1 2 3 4 5].
So our answer is 5.

```md



```

## code
```cpp

int removeDuplicates(vector<int> &arr, int n) {
	// Write your code here.
	int remove = 0;

	for(int i=1;i<n;i++){
		if(arr[i-1] == arr[i]){
			remove++;
		}
	}
	return n-remove;
}

```