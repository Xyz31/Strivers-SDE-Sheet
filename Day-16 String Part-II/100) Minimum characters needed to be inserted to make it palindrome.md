# Minimum characters needed to be inserted to make it Palindrome


```cpp

/*
    Time complexity: O(N ^ 2)
    Space complexity: O(1)
    
    Where N is length of the string.    
*/

// Function for checking a string is palindrome or not
bool isPalindrome(string str)
{
    int l = str.length();
    int i = 0;
    int j = l - 1;

    while (i < j)
    {
        if (str[i] != str[j])
        {
            return false;
        }
        i++;
        j--;
    }
    return true;
}

int minCharsforPalindrome(string str)
{
    int count = 0;

    while (str.length() > 0)
    {
        // If current string is palindrome break the loop
        if (isPalindrome(str))
        {
            break;
        }
        // Otherwise remove the last char and go to next iteration
        else
        {
            count++;
            str.erase(str.begin() + str.length() - 1);
        }
    }
    return count;
}

```


# 
```cpp



/*
int minCharsforPalindrome(string str) {
	// Write your code here.
	
}
*/

#include<bits/stdc++.h>

// Function to calculate the Longest Proper Prefix which is also a Suffix (LPs) array
// Input: a string (str)
// Output: a vector of integers representing the LPs array

vector<int> calculateLPsArray(string str){
    int m = str.length();
    vector<int> lps(m); // LPs array
    int len = 0; // Length of the previous longest proper prefix suffix
    lps[0] = 0; // First element of the LPs array is always 0

    int i = 1;
    while(i < m){
        if(str[i] == str[len]){
            len++;
            lps[i] = len; // Set the LPs value at index i
            i++;
        }else{
            if(len != 0){
                len = lps[len-1]; // Move back to the previous matching position
            }else{
                lps[i] = 0; // No matching prefix found, so set the LPs value at index i to 0
                i++;
            }
        }
    }
    return lps;
}

// Function to calculate the minimum number of characters required to make a string palindrome
// Input: a string (str)
// Output: an integer representing the minimum number of characters to be added

int minCharsforPalindrome(string str) {
    string revstr = str;
    reverse(revstr.begin(), revstr.end()); // Reverse the input string

    string concat = str + "$" + revstr; // Concatenate the original string, a special character '$', and the reversed string

    vector<int> lps = calculateLPsArray(concat); // Calculate the LPs array for the concatenated string

    // The minimum number of characters to be added is the difference between the length of the input string
    // and the value at the last index of the LPs array
    return (str.length() - lps[lps.size()-1]);
}


```