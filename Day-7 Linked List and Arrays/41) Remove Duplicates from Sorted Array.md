# Remove Duplicates from Sorted Array


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