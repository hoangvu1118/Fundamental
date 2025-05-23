**Objective** 
+ s-t Path: Is there a path between vertices s and t?
	+ Traversal
+ Shortest s-t Path: how to find the shortest path between vertices s and t?
	+ Unweighted graph
	+ Weighted graph
	+ `A*`

## s-t Path:
Given source vertex s and a target vertex t, is there a path between s and t?

• Requires us to traverse the graph somehow.
• Start from s and apply traversal until we reach t

### Tree Traversal
**Level Order (Breadth First Traversals)**
+ Visit Top-To-Bottom, Left-To-Right (like reading in English): DBFACEG
**Depth First Traversals** 
+ 3 Types: Preorder, Post-Order, In-Order (Only for binary tree)
+ Basic(rough) idea: Traverse “deep nodes” (e.g. A) before shallow
ones (e.g. F)
![[Pasted image 20250523091806.png | 350]]
Consider the graph as a *tree* and use the same methods BUT NEED *MODIFICATIONS*
#### DFS: Preorder
*Recursive DFS traversal*
```c
dfs(v)
	mark v as visited // PAY ATTENTION
	for(each unvisited vertex u adjacent to v)
		dfs(u)
```
![[Pasted image 20250523091932.png | 400]]
>[!Warning] 
>We don't use **Post-order** and **In-order** for **s-t path problem**
>

>[!Tip] Mark Visited Node
>So each time we traverse to a node, we mark it as **VISITED**
>Then we no longer have to revisited that node in the tree and neglect that path
>
###### Implementation: 


### How to determine the route from s to t ?
Create a table and update the table when we traverse dfs(v)
![[Pasted image 20250523093451.png | 400]]
![[Pasted image 20250523093859.png | 450]]
So every time we traverse, we mark into a table the column **Marked**
Until we reach a node that has no neighbor, and it is not the *destination*
We go back by go to the *edgeTo* column 
--> Continue the process until we find the *destination*
---> Then Traceback from that node to the root to find the path

### BFS - Breadth First Search
By drawing it out like                                                                       
>[!Example] 
>![[Pasted image 20250523100641.png]]

## Shortest path problem
Given: a graph G and vertices s and t
Find: the path which has the shortest length from s to t.

**The length of a path is**:
The number of edges on that path in unweighted graph
• The sum of the edge weights on that path in weighted graph
• Finding the path whose f(t) = 𝑤1 + 𝑤2 + … + 𝑤n is **minimum** with n is the number of edges from s to t
![[Pasted image 20250523102403.png | 450]]
## Unweighted graph: shortest paths
--> Use **BFS to find shortest** paths in this graph
BFS didn’t mention a target vertex, we can stop when we visit target vertex.
• It actually finds the shortest path from s to every vertex.
• **Note**: BFS can be applied to *unweight directed graph* to find the **shortest** path

## Weighted Graphs:
We will make the assumption that the weights on all edges **is a positive number**
• Clearly, if we have negative vertices, it may be possible to end up in a cycle whereby each pass through the cycle *decreases the total length*
• Thus, a ==shortest length== would be undefined for such a graph
• Consider the shortest path from vertex 1 to 4...
• First circle is -1, second circle is -2,…

>[!Tip]
>BFS is *not applied* to weighted graphs
   Dijkstra’s algorithm is a good choice for this case.

## Strategy
Suppose you start at vertex A and A only have three neighbors B, C, and D (the following is a part of weighted graph)
+ You are aware of all vertices adjacent to it
+ This information is either in an adjacency list or adjacency matrix
![[Pasted image 20250523104320.png | 300]]
We accept that the shortest path from A->B: 5 but not sure for (A,C) & (A,D)
![[Pasted image 20250523104818.png | 400]]
![[Pasted image 20250523105306.png | 400]]
--> The minimum(shortest path) which is not replaceable --> mark grey
--> Vertex B && Vertex F

#  Dijkstra's algorithm
We initially don’t know the distance to any vertex except the initial vertex
+ We require an *array of distances*, all *initialized to infinity* except for the *source vertex*, which is *initialized to 0*
+ Each time we visit a vertex, we will examine all adjacent vertices
	+ We need to track visited vertices—a Boolean table of size |V|
+ Do we need to track the shortest path to each vertex?
	+ That is, do I have to store (A, B, F) as the shortest path to vertex F? No

![[Pasted image 20250523105904.png | 400]]
To find the adjacent neighbor of K
![[Pasted image 20250523105956.png | 400]]
Now, we know that H, K form the shortest PATH
![[Pasted image 20250523110038.png | 400]]
