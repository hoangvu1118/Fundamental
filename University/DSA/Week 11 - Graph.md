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
A *sub-graph of a graph* is a subset of the vertices and a subset of the edges that *connected* the subset of vertices in the original graph
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
A graph is a tree if it is connected and there is a *unique* path between any two vertices
![[Pasted image 20250522163612.png | 350]]

>[!tip] Consequences:
>The number of edges is **|E| = |V| – 1**
– The graph is *acyclic*, that is, it *does not contain any cycles*
– Adding one *more edge* must create a *cycle*
– Removing any one edge creates two disjoint non-empty sub-graphs

**Any tree** can be converted into a ROOTED tree by
>[!Tip] Steps:
>- Choosing any vertex to be the root
>-  Defining its neighboring vertices as its children and then recursively defining
>-  All neighboring vertices other than that one designated its
parent are now defined to be that vertices children
![[Pasted image 20250522163938.png]]
## Forest
A **forest** is any graph that has **no cycles**:
>[!Important] Consequences:
>The number of edges is |E| < |V|
>The number of trees = |V| – |E|
>- Removing any one edge adds one more tree to the forest
>- ![[Pasted image 20250522164201.png | 340]]
## Directed Graph
In a directed graph, the *edges on a graph* are be *associated* with a direction
Edges are ordered pairs (vj, vk) denoting a connection from vj to vk
The edge *(vj, vk)* is different from the edge *(vk, vj)*

The maximum number of directed edges in a directed graph is
![[Pasted image 20250522165502.png | 400]]

## In and Out Degrees
The *degree* of a vertex must be *modified to consider both cases:*
+ The *out-degree* of a vertex is the *number of vertices* which are *adjacent* to the given *vertex*
+ The *in-degree* of a vertex is the *number of vertices* which this *vertex is adjacent to*
![[Pasted image 20250522165630.png | 400]]
## Sources and Sinks
**Some definitions:**
– Vertices with an *in-degree of zero* are described as sources
– Vertices with an *out-degree of zero* are described as sinks
In the above `in and out degrees` 
--> Sources: v1, v6, v7
--> Sinks:     v2, v9

## Paths
A path in a *directed graph* is an ordered sequence of vertices 
(v0, v1, v2, ..., vk) 
![[Pasted image 20250522165957.png | 400]]
![[Pasted image 20250522165913.png | 400]]

## Connectedness (Cont.)
Two vertices vj, vk are said to be **connected** if there *exists a path* from vj to vk
+ A graph is *strongly connected* if there *exists a directed path* between any two vertices
+ A graph is *weakly connected* if there *exists a path* between *any two vertices* that ignores the direction
![[Pasted image 20250522170518.png | 400]]

## Weighted undirected graphs
Given a *weighted undirected graph*. In **some cases**, we can consider the graph as weighted directed graph
![[Pasted image 20250522170625.png | 350]]
In a *weighted directed graphs*, each edge is associated with a value
*Unlike* weighted *undirected graphs,* if both *(vj, vk) and (vj, vk)* are edges, it is not required that they have the same weight
![[Pasted image 20250522171009.png | 250]]
## Directed acyclic graphs
A directed acyclic graph is a **directed graph** which has **no cycles**
– These are commonly referred to as **DAGs**
![[Pasted image 20250522171055.png | 250]]![[Pasted image 20250522171108.png | 300]]

>[!Tip] Applications
>– The parse tree constructed by a compiler
>– A reference graph that can be garbage collected using simple reference counting 
>– Dependency graphs such as those used in instruction scheduling and makefiles
>– Dependency graphs between classes formed by inheritance relationships in object-oriented programming languages 
>– Information categorization systems, such as folders in a computer 
>– Directed acyclic word graph data structure to memory efficiently store a set of strings (words)

## Representations - How do we store the adjacency relations?
– Binary-relation list
– Adjacency matrix
– Adjacency list

### Binary-Relation list - The most inefficient 

==A container storing the edges==
{(1, 2), (1, 4), (3, 5), (4, 2), (4, 5), (5, 2), (5, 3), (5, 8), (6, 9), (7, 9), (8, 4)}
![[Pasted image 20250522171427.png | 350]]

### Adjacency Matrix
– The matrix entry (j, k) is set to true if there is an edge (vj, vk)
![[Pasted image 20250522171502.png | 350]]

### Adjacency list - Most efficient for algorithms
*Each vertex* is associated *with a list of its neighbors*
1 • → 2 → 4
2 •
3 • → 5
4 • → 2 → 5
5 • → 2 → 3 → 8
6 • → 9
7 • → 9
8 • → 4
9 •
![[Pasted image 20250522171613.png | 350]]

## The Graph ADT
The *Graph ADT* describes a container storing an *adjacency relation*
– Queries include:
• The number of vertices
• The number of edges
• List the vertices adjacent to a given vertex
• Are two vertices adjacent?
• Are two vertices connected?

– Modifications include:
• Inserting or removing an edge
• Inserting or removing a vertex (and all edges containing that vertex)
==The run-time of these operations will depend on the representation==
