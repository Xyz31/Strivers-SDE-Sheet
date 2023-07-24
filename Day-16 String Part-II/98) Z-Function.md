# Z-Function


```cpp



/*
int zAlgorithm(string s, string p, int n, int m)
{
	// Write your code here
}
*/

// Function to compute the Z array
// Time Complexity: O(N)
void getZArray(const string& concat, vector<int>& z) {
    int n = concat.length();
    int left = 0, right = 0;

    for (int i = 1; i < n; i++) {
        if (i > right) {
            // Case 1: i is outside the Z-box
            left = right = i;
            while (right < n && concat[right - left] == concat[right])
                right++;
            z[i] = right - left;
            right--;
        } else {
            // Case 2: i is inside the Z-box
            int k = i - left;
            if (z[k] < right - i + 1)
                z[i] = z[k];
            else {
                left = i;
                while (right < n && concat[right - left] == concat[right])
                    right++;
                z[i] = right - left;
                right--;
            }
        }
    }
}

// Function to find the number of occurrences of string 'p' in string 's'
// Time Complexity: O(N + M)
int zAlgorithm(const string& s, const string& p, int n, int m) {
    // Build the concatenated string
    string concat = p + "$" + s;
    int concat_length = m + n + 1;

    // Compute Z array
    vector<int> z(concat_length, 0);
    getZArray(concat, z);

    // Count the number of occurrences of 'p' in 's'
    int count = 0;
    for (int i = m + 1; i < concat_length; i++) {
        if (z[i] == m)
            count++;
    }

    return count;
}


```