Data structure consisting of a collection of *Nodes* (*vertices*) interconnected by *edges*
Binary trees are a subset of graphs
- Not all graphs are binary trees
- The terms child, parent, leaf and root have no meaning in graphs
- Graphs don't have specific rules about how nodes are joined
- In a binary tree, all nodes are reachable from the root node

### Where are they used
Mapping problems such as finding the *shortest path*
Modeling websites and their interconnections
Modeling a computer network
Facebook, LinkedIn and Twitter are "social graphs"
Entity Relationship Diagrams
A series of git commits in a repository

### Edges
Connects 2 vertices
Can be directional or not
Might have only directed or undirected, or a mix of both, though it's uncommon
![800](Pasted%20image%2020241028101119.png)

Some graphs might have a disconnected set of nodes
many graphs will have multiple paths to some nodes
A cycle is where you can return to some starting point and repeat a path (looping)

#### Directed and Undirected Edges
Directed - Airline that connects Saskatoon, Edmonton and Calgary
A flight might go from Saskatoon to Edmonton but not from Edmonton to Calgary
A highway usually goes both ways, so using a directed edge is kind of pointless

#### Weight
Weighted graph is one where each edge has some magnitude/cost associated with it
- Distance between 2 cities

Unweighted don't associate any magnitude/cost to an edge
![400](Pasted%20image%2020241028101635.png)

### Sparse vs Dense Graphs
A directed graph with n nodes can have (n-1) edges per node, therefore the total number of edges would be n(n-1)
Undirected graph would have at most half as many as the directed graph, so n(n-1)/2
A graph with few edges compared the maximum is *sparse*
A graph with a number of edges close to the maximum is *dense*
No hard line on sparse - dense
ratio is important when deciding on underlying implementation

### Symbols
`E{v,w}` or `{v,w}` - edge connecting vertex v with vertex w
`{v,w,4}` - Edge between v and w with weight of 4
*V* - set of vertices
*E* - Set of edges
*G* or *(V,E)* - Entire graph, equal to the set of vertices and edges

#### Example 1
`G = (V, E)`
`V = (A, B, C, D)`
`E = ({A,B}, {B, C}, {C, A}, {A, D}`
or `E = ({B, A, 15}, {B, C, 20}, {C, A, 10}, {A, D, 5})` if it's weighted
![](Pasted%20image%2020241028102921.png)

#### Example 2
`V = (Beta, Zeta, Mu, Rho, Chi, Tau)`
`E = ({Beta, Mu, 5}, {Rho, Chi, 3}, {Mu, Rho, 7}, {Tau, Beta, 2}, {Zeta, Beta, 9}, {Chi, Tau, 4})`
![800](Pasted%20image%2020241028103403.png)

#### Example 3
`V = (Paris, London, Rome, Madrid, Berlin)`
`V = Don't have time to write this`
![](Pasted%20image%2020241028103741.png)

### Terminology
*Adjacent*
- Consider a directed edge, A -> B
- vertex B is adjacent to A (Can go from A to B)
- A is **NOT** adjacent to B (can't go from B to A)
- Sometimes called neighbours
- Ones it is directly connected to

*Simple Graph*
- Graph with no loops (vertices connecting to themselves/multiple edges connecting to the same 2 vertices)

*Cycle*
- A path of non-zero length where the first and last vertices are the same
- A graph with no cycles is *Acyclic*
- Paris > London > Madrid > Paris

*Path*
- Sequence of edges that connect two vertices

*Simple Path*
- path that passes through each vertex only once

*Simple Cycle*
- Cycle that passes through every vertex only once

*Subgraph*
- vertices and edges of one part of the graph that is a subset of the whole graph
- Basically just one specific part of the graph

*Spanning Subgraph*
- Subgraph that contains all of the vertices from the whole graph, but not all of the edges - just enough to connect all vertices
- Also called *Spanning tree*

*Connected*
- Undirected graph is connected if there is at least one path from any vertex any other vertex

*Complete Graph*
- A graph that has an edge between every pair of distinct vertices

### Operations
- Add Vertex
- Remove Vertex
- Has Vertex
- Get Vertex
- Enumerate Vertices
- Traversals - Depth first, Breadth first (keep in mind cycles exist, infinite loops)
- Minimum spanning tree
- Shortest Path

## Shortest Weighted Path
Given a graph, what is the shortest path between 2 vertices?
Ex. navigation, networking, logistics, etc.

**Greedy Algorithms**
- make the best possible decision for some part of the problem in the hope that the decision will be best for the overall problem
- once a decision has been made, it is never changed later on
- Used to solve optimization problems
- Don't work for all types of problems

### Dijkstra's Algorithm
Greedy
Only works for undirected, non-weighted graphs
O($n^2$) time complexity

Requires that 3 key prices of information are tracked in each vertex
*Known* - is the shortest path for the start vertex $V_s$ to the current vertex $V$
*Distance* - tentative distance from $V_s$ to the current $V$
*Previous* - the previous vertex on the path to $V_s$

#### Steps
1. From the set of vertices where *known* = false, find the vertex $V$ which has the smallest tentative *distance*
2. Set *known* = true for that vertex
3. For each neighbor ($W$) of $V$ where *known* = false, check $W_{distance} > V_{distance} + cost_{V -> W}$
	1. if it is, set $W_{distance} = V_{distance} + cost$ and also set $W_{previous} = V$

![](Pasted%20image%2020241118103534.png)
