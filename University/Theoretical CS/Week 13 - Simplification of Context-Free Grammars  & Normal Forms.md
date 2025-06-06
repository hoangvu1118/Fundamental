## Methods for Transforming Grammars
![[Pasted image 20250526164927.png | 500]]
![[Pasted image 20250526165034.png | 500]]
![[Pasted image 20250526165045.png | 500]]
## Removing useless productions
One **invariably** wants to remove productions from a grammar that can never take part in any *derivation*.
• Example: in the grammar with P: S → aSb| λ| A 
						    A → aA

The production S → A clearly plays **no role,** as A cannot be transformed into a terminal string.
--> infinite loop

>[!Important] Definition 6.1:
> Let G = (V, T, S, P) be a context-free grammar. A variable **A ∈ V** is said to be useful if and only if there is at least one w ∈ L (G) such that
> ![[Pasted image 20250526211319.png | 300]]
> • In words, a variable is useful if and only if it occurs in **at least one derivation**. 
> • A variable that is not useful is called **useless**. A production is useless if it involves **any useless variable.**

>[!Tip] Steps to remove USELESS
>Two cases in which a variable is useless
>1. Either it *cannot derive* a terminal string: A ==>`*` w ∈ `T*`
>2. Or it *cannot be reached* from the *start* symbol: S ==> * xAy
>![[Pasted image 20250526211721.png | 500]]

![[Pasted image 20250526211829.png]]
**Investigate case 1**: C is an useless variable that *cannot lead to a terminal string*. Therefore, removing C and its corresponding productions
--> G1 with V1 = (S,A,B), terminals T ={a,b}
![[Pasted image 20250526211931.png | 150]]

**Investigate case 2**: Next we want to **eliminate** the variables that **cannot be reached** from the start variable. For this, we can **draw a dependency graph** for the variables
`For context-free grammars, a dependency graph has its vertices labeled with variables, with an edge between vertices C and D if and only if there is a production of the form C → xDy.`
![[Pasted image 20250526212042.png | 400]]  
Just edges without any label 
the final answer is: Grammar 𝐺^= (𝑉^, 𝑇^, S, 𝑃^) with 𝑉^= {𝑆, 𝐴}  ,𝑇^ ={a}, 𝑃^: ![[Pasted image 20250526212055.png | 100]]

>[!Important]
>When every we reducing the *useless* productions
>+ We have to remove sequentially from *case 1* --> *case 2*


>[!Important] Implementation Tips
>Case 1: A is useless as A cannot derive a terminal string 
>--> Remove A and its associated production (2, 3, 4)
>==> P^ : S--> aSb | ab (1, 2)
>         B --> b (5)
> Case 2: Dependency graph of P$^$ below
> --> Draw it out 
> --> B is useless
> ==> Removing B and its associated rules
> P^' : S--> aSb | ab (1, 2)
> Finally, P^'

## Removing $\lambda$ production
>[!Definition]
>![[Pasted image 20250606101031.png | 400]]
>A grammar may generate a language not containing λ, yet have some λ productions or nullable variables. In such cases, the λ-productions can be removed



