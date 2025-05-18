Not all languages all *regular*
Example: L = {a$^n$ b$^n$ : n $\geq$ 0} 
>[!tip] Definition 5.1
>A grammar G = (V,T,S,P) is said to be context-free if all productions in P have the form
>			A --> x
>where A $\epsilon$ V and x $\epsilon$ (V $\cup$ T )* 
>A language L is said to be context-free if and only if there *is a context-free grammar G such that L = L(G)

>[!Important]
>*Every regular grammar is context-free*, so a regular language is also a context-free one
>The family of regular languages is a proper subset of the family of context-free languages

The grammar G ({S}, {a,b}, S, P) with productions
```
	S -> aSa
	S -> bSb
	S -> lambda
```
That is neither right-linear or left-linear is **CONTEXT-FREE** 
This, and similar derivations, make it clear that 





