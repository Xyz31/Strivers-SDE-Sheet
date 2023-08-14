# Compare version numbers

```md



```

```cpp

#include <bits/stdc++.h> 

/*
int compareVersions(string a, string b) 
{
    // Write your code here
}
*/

/*
#include <iostream>
#include <vector>

*/
using namespace std;


// Function: removeZeroesFromEnd
// Description: Removes trailing zeros from a string representing a decimal number.
string removeZeroesFromEnd(string a) {
    int p = a.size() - 1;

    // Iterate backwards by 2 positions at a time
    for (int i = a.size() - 1; i >= 1; i -= 2) {
        // Check if the current character is '0' and the previous character is '.'
        if (a[i] == '0' && a[i - 1] == '.') {
            p -= 2; // Exclude the trailing zeros
        } else {
            break; // Stop iterating if no more trailing zeros found
        }
    }

    return a.substr(0, p + 1); // Return the substring without trailing zeros
}

// Function: compareVersions
// Description: Compares two version strings in the format "x.y.z" and determines their order.
int compareVersions(string a, string b) {
    // Remove trailing zeros from both version strings
    a = removeZeroesFromEnd(a);
    b = removeZeroesFromEnd(b);

    int start1 = 0, start2 = 0, end1 = 0, end2 = 0;

    // Compare version strings character by character
    while (true) {
        // Find the next dot in version string a
        while (end1 < a.size() && a[end1] != '.') {
            end1++;
        }

        // Find the next dot in version string b
        while (end2 < b.size() && b[end2] != '.') {
            end2++;
        }

        // Compare the lengths of the version parts
        if (end1 > end2) {
            return 1; // Version a is greater than version b
        } else if (end1 < end2) {
            return -1; // Version a is less than version b
        }

        // Compare the characters of the version parts
        for (int i = start1; i < end1; i++) {
            if (a[i] > b[i]) {
                return 1; // Version a is greater than version b
            } else if (a[i] < b[i]) {
                return -1; // Version a is less than version b
            }
        }

        // Check if both version strings have been fully compared
        if (end1 == a.size() && end2 == b.size()) {
            return 0; // Version a is equal to version b
        }
        if (end1 == a.size()) {
            return -1; // Version a is less than version b
        }
        if (end2 == b.size()) {
            return 1; // Version a is greater than version b
        }

        // Move to the next version part
        start1 = end1 + 1;
        start2 = end2 + 1;
        end1++;
        end2++;
    }
}




```