# Clone a graph (Not that easy as it looks)


# Approach - I
```cpp

/*
    Time Complexity: O(N + M)
    Space Complexity: O(N)

    Where N is the number of nodes
    and M is the number of edges in the given graph.
*/

#include <unordered_map>

graphNode *cloneGraphHelper(graphNode *node, unordered_map<graphNode *, graphNode *> &copies)
{
	if (node == NULL)
	{
		return NULL;
	}

	// Create a graph node which denotes the node of the cloned graph.
	graphNode *copy = new graphNode(node->data);

	// Update the HashMap.
	copies[node] = copy;

	// Queue used for the BFS.
	queue<graphNode *> level;

	// Push source node.
	level.push(node);

	while (!level.empty())
	{
		// Take the the front element from the queue.
		graphNode *cur = level.front();
		level.pop();

		// Go through all the neighbours.
		for (graphNode *neighbor : cur->neighbours)
		{
			// If it is not present in the HashMap.
			if (copies.find(neighbor) == copies.end())
			{
				copies[neighbor] = new graphNode(neighbor->data, {});
				level.push(neighbor);
			}

			copies[cur]->neighbours.push_back(copies[neighbor]);
		}
	}

	return copy;
}

graphNode *cloneGraph(graphNode *node)
{
	// Create a HashMap.
	unordered_map<graphNode *, graphNode *> copies;

	// Return the source node of cloned graph.
	return cloneGraphHelper(node, copies);
}

```


# Approach - II
```cpp

/*
    Time Complexity: O(N + M)
    Space Complexity: O(N)

    Where N is the number of nodes
    and M is the number of edges in the given graph.
*/

#include <unordered_map>

graphNode *cloneGraphHelper(graphNode *node, unordered_map<graphNode *, graphNode *> &copies)
{
	// If the current node is NULL.
	if (node == NULL)
	{
		return NULL;
	}

	// If HashMap doesn't contain the node.
	if (copies.find(node) == copies.end())
	{
		copies[node] = new graphNode(node->data, {});

		// Go through all the neighbours.
		for (graphNode *neighbour : node->neighbours)
		{
			copies[node]->neighbours.push_back(cloneGraphHelper(neighbour, copies));
		}
	}

	return copies[node];
}

graphNode *cloneGraph(graphNode *node)
{
	// Create a HashMap.
	unordered_map<graphNode *, graphNode *> copies;

	// Return the source node of cloned graph.
	return cloneGraphHelper(node, copies);
}

```