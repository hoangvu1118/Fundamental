## Nondeterministic Pushdown Automata(NPA/ NDPA):
NFA don't have the *stack memory*
![[Pasted image 20250616094817.png | 350]]
Recall finite automata, the program read left to right in the input file, and at the same time change the content in the top of the *stack*
![[Pasted image 20250616095002.png | 450]]
The alphabet and the gamma --> gamma might be different from the alphabet
The top of the stack might be a string of symbols 
![[Pasted image 20250616095622.png | 400]]
Lambda --> do not need to write on to the Stack
cd actually *c* on top and *d* down 1 level
![[Pasted image 20250616100622.png | 400]]
![[Pasted image 20250616100738.png | 200]]
The last element in $\Gamma$ --> every time we read, push down the element like a stack
Notice that transitions are not specified for all possible combinations of input and stack symbols.
• For instance, there is no entry given for δ(q 0 , b, 0). The interpretation for this configuration is the same that we used for nondeterministic finite automata (nfa): An unspecified transition is to the **null set** and represents a **dead** **configuration** for the npda.

Use **Transition Graphs** to represent npda's by l*abelling the edges* of the graph with three things: 
	the current input symbol, 
	the symbol at the top of the stack, 
	and the string that replaces the top of the stack.

![[Pasted image 20250616101321.png | 400]]
## Comment 
**Transition graphs** are convenient for describing npda with the internal state and the input symbol of the string, but they are less useful for keeping track of *stack content*

**The triplet (q, w, u)** is called an ***instantaneous description*** of a pushdown automaton, where 
• q is the state of the control unit, 
• w is the unread part of the input string, 
• u is the stack contents (with the leftmost symbol indicating the top of the stack).

![[Pasted image 20250616102100.png | 500]]

**Moves involving an arbitrary number of steps** will be ![[Pasted image 20250616102330.png | 50]]
![[Pasted image 20250616102352.png | 300]]

![[Pasted image 20250616102430.png | 400]]
]