# Sort an array of 0's, 1's and 2's

### code

```cpp

#include <bits/stdc++.h> 
void sort012(int *arr, int n)
{
   //   Write your code here
   int left,mid,right;
   left=mid=0;
   right=n-1;
   while(mid<=right){
    switch( arr[mid]){
        case 0: swap(arr[left++],arr[mid++]); break;
        case 1: mid++; break;
        case 2: swap(arr[mid],arr[right--]); break;
    }
   }
}

```