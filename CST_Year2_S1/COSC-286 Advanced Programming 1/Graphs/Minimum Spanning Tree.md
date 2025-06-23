# Minimum Spanning Tree
Given a weighted, undirected, connected graph, what is the smallest (by weight/cost) set of edges?
Real world applications are things like laying fiber or pipe to a set of buildings that all need to be connected
Goal - Start with a graph, end up with a minimum spanning tree (remove unnecessary edges)

Why call it "Minimum Spanning Tree" instead of just "Smallest fully connected graph" or something?
- Solution will *always* be a tree because a tree is just a graph with no cycles

## Kruskal's Algorithm
- For a connected undirected weighted graph
- if the graph isn't connected, it can produce a "Minimum Spanning Forest"
- A *Forest* is an undirected graph in which any two vertices are connected by **AT MOST** one path - they may not be connected at all

### Algorithm
1. Get the list of all edges
2. Sort the edge list by weight (lowest to highest)
3. Create a collection of graphs, one for each vertex (**Forest**)
4. While there are still edges in the list and while there is more than one graph in the forest
	1. Remove the edge with minimum weight from the edge list
	2. If the edge connects vertices that are in different graphs, combine the two graphs together using that edge
