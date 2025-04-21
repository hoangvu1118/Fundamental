>[!Definition]
>Two finite accepters, M1 and M2 are said to be equivalent if they both accept the same language
>	L(M1) = L(M2)

![[Pasted image 20250414092209.png | 450]]

• A dfa is a restricted kind of nfa, it is clear that any language that is accepted by a dfa is also accepted by some nfa. 
• There is a language accepted by some nfa for which, in principle, we cannot find a dfa. But it turns out that this is not so. 
• The classes of dfa's and nfa's are equally powerful: For every language accepted by some nfa there is a dfa that accepts the same language

![[Pasted image 20250414092327.png | 500]]
--> there is at least 1 dfa that is equivalent to nfa
## Algorithm to transfer nfa to dfa
![[Pasted image 20250414092500.png | 550]]

explain 3 : choose a node in DFA --> then we assign the number of edges that equal to number of element inside sigma of NFA(which element is used during the process)

![[Pasted image 20250414093440.png| 450]]

## Reduction of the Number of States in Finite Automata
Given two equivalent DFAs below:
![[Pasted image 20250414104826.png | 500]]
*Inaccessible State* : it often appears when we convert NFA to DFA
So it can never *be reached* from the initial state -> q5 as an example
--> Inaccessible state can be **REMOVED** without affecting the language accepted by the automaton
Two things are optimized -> Execution Time and Storage

### Distinguishable vs Indistinguishable
![[Pasted image 20250414105320.png | 450]]
*TWO STATES* are either distinguishable or indistinguishable 
• Indistinguishability has the properties of an equivalence relation: **If p and q are indistinguishable and if q and r are also indistinguishable, then so are p and r, and all three states are indistinguishable.** 
• One method for *reducing the states of a dfa* is based on *finding and combining indistinguishable states.*
• A method for finding pairs of *Distinguishable* states
![[Pasted image 20250414110217.png | 550]]
![[Pasted image 20250414110403.png | 550]]

**Algorithm for solving "states reduction"**

First for 0 equivalence, we have 2 distinguishable sets
- For each set that has more than 2 elements, we have to investigate 'em
+ Example: 0-Equivalence : {q0} {q1,q2,q3}
	+ We gonna investigate the 2nd set
		+ Checking each pair : (q1,q2) (q1,q3) (q2,q3)
		+ However, if you check and see that q1 ,q2 are equivalent 
		+ then we do not have to check (q2,q3)
		+ So by using the 0-equivalence -> we can from that construct 1 equivalence
		+ By checking the state at which these nodes move 
			+ Ex: q1-a> q3 ... q2-b> q1
			+ If for "a" or "b" the 2 nodes are in different set (taken from previous equivalence) 
			+ Then they're distinguishable

