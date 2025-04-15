## Reason to learn Tree structure
Efficient Data organization
+ File directories, organizational charts
Representation of Hierarchical Data
+ Family trees, decision trees
Fast Search and Retrieval
+ BST, AVL tree
Foundational Knowledge for Advanced Concepts
+ Graph, priority Queues

Almost all operations on tree : insert, delete, search ==> O(logn)

## Formal Definition
A tree is a collection of nodes
Starting Node known as Root Node
Every node other than the root has a *parent node*
Nodes may have *any number of children*
Nodes with *no children* are known as *leaves*

**Path**
A path to *a node* is a sequences of nodes root, n1, n2 ... such that n1 is a child of root, n2 is child of n1.....
--> There is one *PATH* from root to Node in *TREE*

**DEPTH** of a node is the length of the unique path from the root to the node *(not counting the node -> exclusive)*
![[Pasted image 20250415092255.png | 400]]
Consider this tree-> Depth to E = *2*
Root is at depth 0

**HEIGHT** of a non-leaf node is the length of the LONGEST path from node to a leaf(*not counting the leaf*) 
Height of a leaf = 0
Height of A = 2

![[Pasted image 20250415092928.png | 400]]![[Pasted image 20250415092939.png | 400]]
![[Pasted image 20250415093201.png | 400]]
Explanation for above images
>[!LUCKY]
>Fortunately, CompSci student dont have to study such trees 
>We only care about Binary Trees -> Which have only 2 children per node

**Delete of a child B**
Then all of the children of B will become the children of the Root ![[Pasted image 20250415093434.png | 300]]

**Addition of a child**
Create the new child node
Add a pointer to this child in the link list of its parents

**Deletion of a root**
One of the children becomes the new root
Other children of old root become the children of the new root

![[Pasted image 20250415093713.png | 300]] ![[Pasted image 20250415093719.png | 300]]

Look from right --> left

## Tree Traversal (Tree search)
Many algorithms involve walking through a tree, and performing some computation at each node
Walking through a tree is called *traversal*

Two ways : DFS and BFS
*Depth-First Search(DFS)*:
+ Pre-order 
+ Post-order
+ In-order (Applied in Binary Tree)
*Breadth-First Search* or Level-order Tree

![[Pasted image 20250415094214.png |300]]
*Start always from a ROOT*

**DFS- pre-order**
First **visit a node,** then with its children 
+ Visit : performing some computation at this node 
A→B→E→F→C→G→D
==ROOT -> LEFT -> RIGHT==
**DFS - Post-Order**
First **visit its children**, then return to node 
+ Similar to visit in pre-order
Again, we still starts with a Root A but we don't visit them, we just go through
--> so actually we traverse to E(leaves) -> we start computing from leaves up to A
E→F→B→G→C→D→A
==LEFT->RIGHT->ROOT==
**BFS**:
Visit all nodes at the current level before moving to the next level 
Ignoring the order of that level 
A → B→C→D→E→F -> D
In second layer -> we can either go B C D or D C B

## Binary Tree
A node can have *at most* 2 children :
+ Left child 
+ Right child

The largest DEPTH of a binary tree of N nodes : **N - 1** | Worst Case
**Worst-Case binary Tree** : linear Tree
![[Pasted image 20250415094858.png | 150]]
**Best-Case** Every node have 2 children
-> The depth is O(logN)

## In-order Traversal
![[Pasted image 20250415095349.png | 500]]
==LEFT -> ROOT -> RIGHT==
