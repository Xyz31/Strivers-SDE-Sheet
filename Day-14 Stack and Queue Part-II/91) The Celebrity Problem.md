# The Celebrity Problem


# Approach - I
```cpp

/*
    Time complexity: O(N*N)
    Space complexity: O(N)
	
    Where 'N' is the number of people at the party.
*/

int findCelebrity(int n) {

    // Calculating indegree and outdegree of each nodes.
    vector<int> indegree(n), outdegree(n);

    for(int i = 0; i < n; i++) {
        for(int j = 0; j < n; j++) {
            if(knows(i, j)) {
                indegree[j]++;
                outdegree[i]++;
            }
        }
    }

    // Finding Celebrity.
    int celebrity = -1;

    for(int i = 0; i < n; i++) {
        if(indegree[i] == n - 1 && outdegree[i] == 0) {
            celebrity = i;
            break;
        }
    }

    return celebrity;
}

```

# Approach - II
```cpp

/*
    Time complexity: O(N*N)
    Space complexity: O(1)
    
    Where 'N' is the number of people at the party.
*/

int findCelebrity(int n) {
    
    int celebrity = -1;

    // Check one by one whether the person is a celebrity or not.
    for(int i = 0; i < n; i++) {
        bool knowAny = false, knownToAll = true;

        // Check whether perosn with id 'i' knows any other person.
        for(int j = 0; j < n; j++) {
            if(knows(i, j)) {
                knowAny = true;
                break;
            }
        }

        // Check whether perosn with id 'i' is known to all the other person.
        for(int j = 0; j < n; j++) {
            if(i != j and !knows(j, i)) {
                knownToAll = false;
                break;
            }
        }

        if(!knowAny && knownToAll) {
            celebrity = i;
            break;
        }
    }

    return celebrity;
}

```

# Approach - III
```cpp

/*
    Time complexity: O(N)
    Space complexity: O(N)
    
    Where 'N' is the number of people at the party.
*/

#include <stack>

int findCelebrity(int n) {

    // Create a stack and push all ids in it.
    stack<int> ids;
    for(int i = 0; i < n; i++) {
        ids.push(i);
    }

    // Finding celebrity.
    while(ids.size() > 1) {
        int id1 = ids.top();
        ids.pop();
        int id2 = ids.top();
        ids.pop();
        
        if(knows(id1, id2)) {
            // Because person with id1 can not be celebrity. 
            ids.push(id2); 
        }
        else {
            // Because person with id2 can not be celebrity.
            ids.push(id1); 
        }
    }

    int celebrity = ids.top();
    bool knowAny = false, knownToAll = true;

    // Verify whether the celebrity knows any other person.
    for(int i = 0; i < n; i++) {
        if(knows(celebrity, i)) {
            knowAny = true;
            break;
        }
    }

    // Verify whether the celebrity is known to all the other person.
    for(int i = 0; i < n; i++) {
        if(i != celebrity and !knows(i, celebrity)) {
            knownToAll = false;
            break;
        }
    }

    if(knowAny or !knownToAll) {
        // If verificatin failed, then it means there is no celebrity at the party.
        celebrity = -1;
    }

    return celebrity;
}

```

# Approach - IV
```cpp

#include <bits/stdc++.h> 
/*
	This is signature of helper function 'knows'.
	You should not implement it, or speculate about its implementation.

	bool knows(int A, int B); 
	Function 'knows(A, B)' will returns "true" if the person having
	id 'A' know the person having id 'B' in the party, "false" otherwise.
*/

/*
T-O(N)
S-O(1)
*/
int findCelebrity(int n) {
    int candidate = 0; // Initialize the candidate as the first person
    
    // Loop through each person from the second person to the last
    for (int i = 1; i < n; i++) {
        if (knows(candidate, i))
            candidate = i; // If the candidate knows the current person, update the candidate
    }
    
    // Check if the candidate is a valid celebrity
    for (int i = 0; i < n; i++) {
        if (i != candidate && (knows(candidate, i) || !knows(i, candidate)))
            return -1; // Return -1 if the candidate knows someone or someone doesn't know the candidate
    }
    
    return candidate; // Return the candidate ID if found
}


```