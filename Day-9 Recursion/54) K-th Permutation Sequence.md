# K-th Permutation Sequence

Sample Input 1:
2
2 1
3 6


Sample Output 1:
12
321


Explanation For Sample Output 1:
For the first test case, ‘N’ = 2. So all permutations are “12”, “21”. Now ‘K’ = 1, so the 1st permutation is “12”.

For the second test case, ‘N’ = 3. So all permutations are  “123”, “132”, “213”, “231”, “312”, “321”. Now ‘K’ = 6, so the 6th permutation is “321”.

```md



```

## code
```cpp

string kthPermutation(int n, int k) {
    int fact = 1;
    vector<int> numbers;
    
    // Create a vector of numbers from 1 to n
    for (int i = 1; i <= n; i++) {
        numbers.push_back(i);
        fact *= i; // Calculate the factorial of n
    }

    //fact = (n-1)!
    fact = fact/n;

    string ans = "";
    k = k - 1; // Decrement k by 1 to handle zero-based indexing
    while (true) {
        ans += to_string(numbers[k / fact]); // Append the selected number to the answer string
        
        // Remove the selected number from the vector
        numbers.erase(numbers.begin() + (k / fact));

        if (numbers.size() == 0) {
            break; // Exit the loop if all numbers have been selected
        }

        k = k % fact; // Update k to the remainder after division by the factorial
        fact = fact / numbers.size(); // Update the factorial by dividing it by the reduced size of the vector
    }

    return ans;
}

```