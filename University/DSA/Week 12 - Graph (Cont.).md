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



