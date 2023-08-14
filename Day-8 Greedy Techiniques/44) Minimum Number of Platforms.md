# Minimum Number of Platforms

Sample Input 1:
2
6
900 940 950 1100 1500 1800
910 1200 1120 1130 1900 2000
4
100 200 300 400
200 300 400 500


Sample Output 1:
3
2


Explanation Of The Sample Output 1:
In test case 1, For the given input, the following will be the schedule of the trains:

Train 1 arrived at 900 on platform 1. 
Train 1 departed at 910 from platform 1. 
Train 2 arrived at 940 on platform 1.
Train 3 arrived at 950 on platform 2 (since platform 1 was already occupied by train 1).
Train 4 arrived at 1100 on platform 3 (since both platforms 1 and 2 were occupied by trains 2 and 3 respectively).
Train 3 departed at 1120 from platform 2 (platform 2 becomes vacant).
Train 4 departed at 1130 from platform 3 (platform 3 also becomes vacant).
Train 2 departed at 1200 from platform 1 (platform 1 also becomes vacant).
Train 5 arrived at 1500 on platform 1.
Train 6 arrived at 1800 on platform 2.
Train 5 departed at 1900 from platform 1.
Train 6 departed at 2000 from platform 2.

Thus, minimum 3 platforms are needed for the given input.

In test case 2, For the given input, the following will be the schedule of the trains:

Train 1 arrived at 100 on platform 1. 
Train 2 arrived at 200 from platform 2 (as platform 1 is occupied by train 1).
Train 1 departed at 200 from platform 1. 
Train 3 arrived at 300 on platform 1.
Train 2 departed at 300 from platform 2.
Train 4 arrived at 400 on platform 2.
Train 3 departed at 400 from platform 1.
Train 4 departed at 500 from platform 2. 

Thus, 2 platforms are needed for the given input.

```md



```

## code 
```cpp

struct Train{
    int arrival;
    int departure;
    int pos;
};


bool compare(Train t1, Train t2) {
    if (t1.departure < t2.departure) return true;
    if (t1.departure > t2.departure) return false;
    if (t1.pos < t2.pos) return true;
    return false;
}


int calculateMinPatforms(int at[], int dt[], int n) {
    // Write your code here.

    
    sort(at,at+n);
    sort(dt,dt+n);
 
    int ans=1;
    int count=1;
    int i=1,j=0;
    while(i<n && j<n)
    {
        if(at[i]<=dt[j]) //one more platform needed
        {
            count++;
            i++;
        }
        else //one platform can be reduced
        {
            count--;
            j++;
        }
        ans=max(ans,count); //updating the value with the current maximum
    }
    return ans;// Return the minimum number of platforms required.

}


```