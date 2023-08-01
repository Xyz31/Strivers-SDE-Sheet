# Find Median in a stream of Integers


# Approach - I Brute force approach
```cpp

/*

	Time complexity: O(N*(N*log(N))) 
	Space complexity: O(N)
	
	where N is the total number of elements in the array.

*/

#include <algorithm>

vector<int> findMedian(vector<int> &arr, int n){
	
	// To store the incoming stream elements
	vector<int>store;
	
	// To store the medians
	vector<int> medians;
	
	for(int i = 0; i < n; i++){
		
		// Storing the incoming data from stream in a vector 'store'
		store.push_back(arr[i]);
		
		// Sorting the vector to arrange all the elements in sorted order
		sort(store.begin(),store.end());
		
		int median;
		// Even number of elements are read, (Note - 0 based indexing is used)
		if((i+1)%2==0){
			
			// Average of middle two values
			median = (store[i/2] + store[(i+1)/2])/2;
				
		}
		// odd number of elements are read
		else{
			
			// The middle value of the sorted arrangement of the elements read so far
			median = store[i/2];
			
		}
		
		medians.push_back(median);
		
	}
	
	return medians;
}


```

# Approach - II Insertion sort approach
```cpp

/*

	Time complexity: O(N*N) 
	Space complexity: O(N)
	
	where N is the total number of elements in the array.

*/

vector<int> findMedian(vector<int> &arr, int n){
	
	//To store the incoming elements
	vector<int> store;
	
	// To store the medians
	vector<int> medians;
	
	for(int i = 0; i < n; i++){
		
		// Insert the new element in the store vector 
		store.push_back(arr[i]);
		
		// shift it at its sorted position in store
		int j = 0;
		
		while(j < i){
			
			if(store[j] <= arr[i]){
				j++;	
			}
			else{
				break;
			}
			
		}
		
		// Shifting all the elements greater than the current element to the right 
		
		int k = i-1;
		
		while(k >= j){
			
			store[k+1] = store[k];
			k--;
			
		}
		
		// Inserting the current element at its sorted position
		store[j] = arr[i];
			
		int median;
		// Even number of elements are read, (Note - 0 based indexing is used)
		if((i+1)%2==0){
			
			// Average of middle two values
			median = (store[i/2] + store[(i+1)/2])/2;
				
		}
		// odd number of elements are read
		else{
			
			// The middle value of the sorted arrangement of the elements read so far
			median = store[i/2];
			
		}
		
		medians.push_back(median);
				
	}
	
	return medians;
}


```


# Approach - III Heap based approach
```cpp

/*

	Time complexity: O(N*(log(N))) 
	Space complexity: O(N)
	
	where N is the total number of elements in the array.

*/

#include <queue>

vector<int> findMedian(vector<int> &arr, int n){
	
	// To store the medians
	vector<int> medians;
	
	// max heap
	priority_queue<int> lo;  
	
	//min heap                            
    priority_queue<int, vector<int>, greater<int>> hi;   
    
    for(int i = 0; i < n; i++){
    	
    	int num = arr[i];
    	
    	// Add to max heap
    	lo.push(num);                                
		
		// Balancing step, that is inserting the current element at its position that is either less than median or more than median value
        hi.push(lo.top());                        
        lo.pop();

		// Maintain size property, as 'lo' can have utmost one more element than 'hi' or both have equal number of elements
        if (lo.size() < hi.size()) {                    
            lo.push(hi.top());
            hi.pop();
        }
        
        int median;
        
        // For odd number of elements
        if(lo.size() > hi.size()){
        	
        	median = lo.top();
        	
		}
		// For even number of elements
		else{
			
			median = (lo.top() + hi.top())/2;  
			
		}
        
    	medians.push_back(median);
	}
	
	return medians;

	
}



```