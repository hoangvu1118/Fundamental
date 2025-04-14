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
