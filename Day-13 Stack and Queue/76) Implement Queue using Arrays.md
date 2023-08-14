# Implement Queue using Arrays

```md



```

```cpp

#include <bits/stdc++.h> 



class Queue {
    int* arr;
    int start, end;

public:
    Queue()
    {
        arr = new int[5001]; // Required size
        start = 0;
        end = 0;
    }

    bool isEmpty()
    {
        return start == end;
    }

    void enqueue(int data)
    {
        arr[end++] = data;
    }

    int dequeue()
    {
        if (!isEmpty())
            return arr[start++];
        return -1;
    }

    int front()
    {
        if (!isEmpty())
            return arr[start];
        return -1;
    }
};

```