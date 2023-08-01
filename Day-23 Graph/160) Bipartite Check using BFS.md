# Bipartite Check using BFS


# Approach - I
```cpp

/*
	Time Complexity : O(N * N)
	Space Complexity : O(N)

	Where 'N' is the number of nodes in the graph.
*/

#include <queue>

bool isGraphBirpatite(vector<vector<int>> &edges) {
	int n = edges.size();

	vector<vector<int>> graph(n);

	for (int i = 0 ; i < n ; i++) {
		for (int j = 0 ; j < n ; j++) {
			if (edges[i][j]) {
				graph[i].push_back(j);
				graph[j].push_back(i);
			}
		}
	}

	vector<int> color(n, -1);

	// Marking the color of root as 0.
	for (int i = 0 ; i < n ; i++) {
		if (color[i] != -1) {
			continue;
		}
		color[i] = 0;

		queue<int> que;

		que.push(i);
		int c = 0;

		while (!que.empty()) {
			int node = que.front();
			que.pop();

			// Traversing all the neighbours of the current node.
			for (int nbr : graph[node]) {
				if (color[nbr] != -1 and color[nbr] == color[node]) {
					return false;
				} else if (color[nbr] == -1) {
					color[nbr] = !color[node];
					que.push(nbr);
				}
			}
			c = !c;
		}
	}

	return true;
}


```


