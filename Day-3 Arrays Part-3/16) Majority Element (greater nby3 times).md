# Majority Element (>n/3 times)


### code

```cpp

#include <bits/stdc++.h>

using namespace std;

vector<int> majorityElementII(vector<int> &nums)
{
    int s = nums.size();
    int num1 = -1, num2 = -1;
    int c1 = 0, c2 = 0;

    // Finding the two most frequently occurring elements
    for (auto x : nums)
    {
        if (num1 == x)
            c1++;
        else if (num2 == x)
            c2++;
        else if (c1 == 0 && x != num2)
        {
            num1 = x;
            c1++;
        }
        else if (c2 == 0 && x != num1)
        {
            num2 = x;
            c2++;
        }
        else
        {
            // Decrementing the count for both elements
            c1--;
            c2--;
        }
    }

    vector<int> ans;
    c1 = c2 = 0;

    // Counting occurrences of the two elements
    for (auto x : nums)
    {
        if (num1 == x)
            c1++;
        else if (num2 == x)
            c2++;
    }

    // Checking if the counts are greater than n/3
    if (c1 > s / 3)
        ans.push_back(num1);
    if (c2 > s / 3)
        ans.push_back(num2);

    return ans;
}


```