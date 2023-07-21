# Minimum Number of Platforms


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