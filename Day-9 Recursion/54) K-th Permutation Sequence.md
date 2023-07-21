# K-th Permutation Sequence


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