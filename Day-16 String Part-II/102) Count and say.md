# Count and say


```cpp

#include <bits/stdc++.h> 

/*
string writeAsYouSpeak(int n) 
{
	// Write your code here.	
}

*/


string build(string num){
	int freq = 1; // Number of occurrences of the current digit
	char curNum = num[0]; // Current digit
	string res=""; // Resulting string

	for(int i=1;i<num.size();i++){
		if(curNum == num[i]){
			freq++; // Increment frequency if the current digit is the same as the previous digit
		}else{
			char frq = (char)('0'+freq); // Convert the frequency to a character
			res.push_back(frq); // Append the frequency character to the result
			res.push_back(curNum); // Append the current digit to the result

			curNum = num[i]; // Update the current digit to the next digit
			freq = 1; // Reset the frequency for the new digit
		}
	}

	char frq = (char)('0'+freq); // Convert the final frequency to a character
	res.push_back(frq); // Append the frequency character to the result
	res.push_back(curNum); // Append the last digit to the result

	return res; // Return the resulting string
}

string writeAsYouSpeak(int n){

	string initial = "1"; // Start with the initial value "1"
	for(int i=0;i<n-1;i++){
		initial = build(initial); // Build the next sequence based on the previous sequence
	}
	return initial; // Return the final sequence
}


```