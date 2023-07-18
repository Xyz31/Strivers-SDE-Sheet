# Pow(x, n) - Modular Exponentiation

### code

```cpp

#include <bits/stdc++.h>

int modularExponentiation(int a, int b, int m) {
	// Compute (a^b) % m using modular exponentiation

	int ans = 1; // Initialize the result to 1

	while (b > 0) {
		if (b & 1) {
			// If the current bit of b is set (i.e., odd power),
			// multiply ans with a and take modulo m
			ans = (ans * 1LL * a) % m;
		}

		// Square a and take modulo m for the next power
		a = (a * 1LL * a) % m;

		// Right shift b by 1 to consider the next bit
		b >>= 1;
	}

	return ans; // Return the computed result (a^b) % m
}


```