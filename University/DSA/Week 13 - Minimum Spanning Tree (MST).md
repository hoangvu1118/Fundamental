Given an undirected graph, **a spanning tree T** is a subgraph of G, where T:
● Is connected.
● Is acyclic. (non-cycle)
● Includes all of the vertices.

Example:
● Spanning tree is the black edges and vertices.
	A minimum spanning tree is a spanning tree of minimum total weight.
● Example: Network of power lines that connect a bunch of buildings.

These two properties make it a tree --> This makes it spanning
![[Pasted image 20250530110502.png | 250]]   ![[Pasted image 20250530110855.png | 250]]

The MST(minimum spanning tree) is different from the SPT(shortest path tree) (one node to every other node)

A *shortest paths tree* depends on the *start vertex:*
● Because it tells you how to get from a source to EVERYTHING.
There is **no source** for a MST.

Nonetheless, the MST sometimes happens to be an SPT for **a specific vertex.**
For a **weighted undirected graph**, there is only **1 MST** and the number of edges of a MST **is V-1** if its edge weights are unique.

## Finding Union --> Cycle
![[Pasted image 20250530150727.png]]

## Algorithm 
Basic : Just random cut
Start with no edges in the MST.
● Find a cut that has no crossing edges in the MST.
● Add smallest crossing edge to the MST.
● Repeat until MST has V-1 edges.
This should work, but we need some way of finding a cut with no crossing edges!
● Random isn’t a very good idea

### Prim's Demo
![[Pasted image 20250530152302.png | 450]]
### Optimized Prim's --> Using Priority Queue
