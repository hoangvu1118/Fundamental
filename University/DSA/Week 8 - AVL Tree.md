A Tree which we can make sure that its height is always O(logN)
With N is number of node

AVL trees : Balance is *defined* by *comparing the height* of the two subtrees
>[!Warning] Height of tree
>+ An empty tree has height *-1*
>+ A tree with a single node has height *0*

>[!tip] AVL Tree
>A binary tree is *said to be AVL balanced* if :
>+ The difference btw the heights btw the *left and right* subtree is at most 1
>+ Both subtrees are themselves *AVL trees*
>
> ![[Pasted image 20250422103540.png]]
> The 2 picture -> Right has height 0 | Left has height -1 -> still balanced

We want to make sure all of the node are balanced
![[Pasted image 20250422103805.png]]

## Operations in AVL Tree
### Insertion and Deletion
>[!Remember] Maintain AVL balance
>Inserting a node can increase the height of a tree by at most 1
>Removing a node can decrease the height of a tree by at most 1

![[Pasted image 20250422104502.png | 350]]
17 --> right has height = 1 
	-> left has height = -1 
Imbalance

36 -> right has height  = 1
	-> left has height = 3
Imbalance

Here, we encounter *two imbalance node 17 & 36*
However, we only need to fix the node 17 -> the last node
![[Pasted image 20250422105056.png | 250]]

## Ways of maintaining balance
>[!Def] 
>If an insertion *causes an imbalance*, node can be affected : **Nodes on path of the inserted node**
>Let f be the node that must be *rebalanced*
>
>Case 1: insertion in the left subtree of the left child of f 
>Case 2: insertion in the right subtree of the left child of f 
>Case 3: insertion in the left subtree of the right child of f 
>Case 4: insertion in the right subtree of the right child of f
>
>Case 1 and 4 : Same ( Similar for 2 and 3)

## Case 1 and 4 : Single Rotation

![[Pasted image 20250422111200.png]]
Easily spotted that *36* is imbalance since left height : 3 and right height : 1
So we want to rotate, which makes *12* to be a root 
This case is *insert left subtree of the left child*
So we take the right subtree of the left child out (which is node *23*) assign it to temp node
Then we point 12->right to point to the *former root 36* 
And then *36->left* point to that *temp node* which make the *12* become root 
and make it balance
-> Case 1 : Rotate right 
-> Case 4 : similar but we rotate it Lefty

>[!Success] Algorithm
>Step 1 : Find the imbalance node
>Step 2 : Fix the latest node


## Case 2: Double Rotation

