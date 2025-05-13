A graph is an abstract data type for storing adjacent relations
>[!Definition] Undirected Graph ADT
>+ V = {v1, v2, v3, ....}
>+ The number of vertices is denoted by |V| = n
>+ Associated with this is a collection E of unordered pairs {vi, vj} termed edges which connect the vertices

There are a number of data structures that can be used to implement abstract undirected graphs
– Adjacency matrices
– Adjacency lists

>[!Tip] Example
>|V| = 9
>![[Pasted image 20250513105005.png | 300]]![[Pasted image 20250513105146.png | 300]]

## Degree 
*The number of adjacent vertices* or neighbors
![[Pasted image 20250513105309.png | 300]]

## Sub-Graphs
A *sub-graph of a graph* is a subset of the vertices and a subset of the edges that connected the subset of vertices in the original graph
![[Pasted image 20250513105643.png | 350]]

## Paths
A path in an undirected graph is an ordered sequence of vertices (v0, v1, v2, ..., vk)

```
where {vj – 1, vj} is an edge for j = 1, ..., k 
– Termed a path from v0 to vk
– The length of this path is k
```

>[!Example]
>![[Pasted image 20250513105841.png | 300]]

**Trivial Path** : A path at the vertex location --> (A) = 0
## Simple Path
A *simple path* has *no repetitions* other than perhaps the first and last vertices
A *simple cycle* is a simple path of `at least two vertices` with the `first and last vertices` equal`

## Connectedness 
Two vertices *vi, vj are said to be connected* if there exists a path from vi to vj
A *graph is connected* if there exists a path between *any two vertices*
![[Pasted image 20250513110254.png | 350]]

## Weighted Graphs
A *weight* may be associated with *each edge in a graph*
– This could represent **distance, energy consumption, cost, etc.**
– Such a graph is called a weighted graph Pictorially, we will represent weights by numbers next to the edges
![[Pasted image 20250513110528.png | 250]]  ![[Pasted image 20250513110540.png | 250]]![[Pasted image 20250513110609.png | 300]]
Problem: **find the shortest path between two vertices**
– Here, the shortest path from A to G is (A, C, F, D,E, G) with length 5.7

## Trees

## Forest

## Directed Graph

## Sources and Sinks
