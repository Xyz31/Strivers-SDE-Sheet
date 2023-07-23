# Check for balanced parentheses


```cpp

#include <vector>

/*
    Time Complexity : O(N)
    Space Complexity : O(N)

    Where 'N' is the length of the string.
*/

// Function to check if the given input string contains valid parentheses.
bool isValidParenthesis(string s)
{
    // Create a vector to act as a stack to store opening parentheses.
    vector<int> stacks;
    
    // Iterate through the characters of the input string.
    for (int i = 0; i < s.size(); i++) {
        // If the current character is an opening parenthesis ('(', '[', '{'),
        // push it onto the stack.
        if (s[i] == '(' || s[i] == '[' || s[i] == '{') {
            stacks.push_back(s[i]);
        } else {
            // If the current character is a closing parenthesis (')', ']', '}'),
            // check if the stack is empty. If it is, return false as there is
            // no matching opening parenthesis for the current closing parenthesis.
            if (stacks.empty()) {
                return false;
            }

            // If the stack is not empty, check if the top of the stack (the last element)
            // matches the current closing parenthesis. If they match, pop the opening
            // parenthesis from the stack, as they form a valid pair.
            if (s[i] == ')' && stacks.back() == '(') {
                stacks.pop_back();
            } else if (s[i] == ']' && stacks.back() == '[') {
                stacks.pop_back();
            } else if (s[i] == '}' && stacks.back() == '{') {
                stacks.pop_back();
            } else {
                // If the top of the stack and the current closing parenthesis do not match,
                // return false, as it means the parentheses are not balanced.
                return false;
            }
        }
    }
    
    // After the loop finishes, check if the stack is empty. If it is, that means
    // all the opening parentheses have been matched and popped, and the input string
    // contains valid parentheses. In this case, return true; otherwise, return false.
    if (stacks.empty() == true)
        return true;
    return false;
}


```