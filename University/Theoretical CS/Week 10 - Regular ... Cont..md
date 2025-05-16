### Theorem 3.2 
L is a regular language. Then there exists a regular expression *r* such that L = L(r)
![[Pasted image 20250505092830.png]]
We need it to stop so the program should stop at qf since it has *
The ring (r4 + r3r1* r2)* might cause confusion
But just imagine *that* is an hidden ring but it use r1 from q0 so we do not have to draw it out like below images
![[Pasted image 20250421114429.png | 200]]
Remember this one
R = P + RQ
R = QP*

![[Pasted image 20250505093836.png | 400]]

Regular Expressions for *Describing Simple Patterns* 
+ Identifiers, or integers and real numbers in many programming languages. 
+ Regular expression sdd * , where s stands for the sign, with possible values from {+ , -, λ}, 
and d stands for the digits 0 to 9
`Used in pattern-matching editor:
`The vi editor in the UNIX operating system recognizes the command /aba*c/ as an instruction to search the file for the first occurrence of the string ab, followed by an arbitrary number of a’s, followed by a c`

## Regular Grammar
• Right- and Left-Linear Grammars
• Right-Linear Grammars Generate Regular Languages 
• Right-Linear Grammars for Regular Languages 
• Equivalence of Regular Languages and Regular Grammars

### Right and Left Linear Grammars

**Definition 3.3:**
A grammar *G = (V, T, S, P)* is said to be *right-linear* if *all* productions are of the form
	A → x==B==, 
or    A → x,
where A, B ∈V, and x ∈T * 

A grammar is said to be *left-linear if all* productions are of the form 
	A → ==B==x, 
or     A → x. 
A regular grammar is one that is **either right-linear or left-linear**

>[!Example]
>![[Pasted image 20250505101717.png | 450]]
>Rules ~~ Production  ~~ Condition
>If the 'S' is a mixed, neither right linear or left linear then IT IS NOT REGULAR GRAMMARS

The sequence S => abS => ababS => ababa is a *derivation* with G1.
From this single instance it is easy to conjecture that L(G1) is the language denoted by the regular expression **r = (ab)* a***

In a similar way, we can see that L(G2) is the regular language **L(aab(ab)* )***

**Linear Grammar** 
The grammar G = ({S, A, B}, {a, b}, S, P) with productions
S → A, 
A → aB| λ, 
B→ Ab,
is *not* regular. Although every production is either right-linear or left-linear
However, the grammar itself is *neither right nor left* --> not regular
>[!Definition]
>A linear grammar is a grammar in which at most one variable can occur on the right side of any production, without restriction on the position of this variable.


**Right-Linear Grammars Generate Regular Languages**
**Theorem 3.3:** Let G = (V, T, S, P) be a right-linear grammar. Then, L(G) is a regular language.![[Pasted image 20250505103141.png]]
![[Pasted image 20250505103150.png]]
>[!Example]
>![[Pasted image 20250505103208.png | 350]]

**Theorem 3.4**: If L is a regular language on the alphabet $\sum$ then there exi[[]]sts a right-linear grammar G = (V, $\sum$, S, P) such that L = L(G).
![[Pasted image 20250505105228.png | 400]]
![[Pasted image 20250505105244.png | 400]]

![[Pasted image 20250516100604.png | 450]]
