
>[!Tip] Definition 5.2:
> A derivation is said to be *leftmost if in each step* the leftmost variable in the sentential form is replaced. If in each step the *rightmost variable is replaced*, we call the *derivation rightmost*
> ![[Pasted image 20250525201518.png | 400]]
In order to show which production is applied, we have numbered the productions and written the appropriate number on the symbol “⇒”. 
• From this we see that the two derivations not only yield the same sentence but also use exactly the same set of productions. The difference is entirely in the order in which the productions are applied


## Derivation Trees
+ A second way of showing derivations, **independent of the order** in which productions are used, is by a *derivation or parse tree.* 
+ A derivation tree is *an ordered tree* in which *nodes* are labeled with *the left sides* of productions and in which the *children of a node represent* its corresponding *right sides.*
+ ![[Pasted image 20250525201656.png | 350]]

>[!Important] Definition 5.3: 
>Let G = (V, T, S, P) be a context-free grammar. An ordered tree is a derivation tree for G if and only if it has the following properties. 
>1. The root is labeled **S.** 
>2. Every leaf has a label from **T ∪ {λ}.** 
>3. Every **interior vertex** (a vertex that is **not a leaf)** has **a label from V.** 
>4. If a vertex has label **A ∈ V,** and its children are labeled **(from left to right) a1, a2, …, an** , then P must contain a production of the form: A --> a1, a2, ..., an 
>5. A **leaf** labeled λ has **no siblings**, that is, a vertex with a child labeled λ can have no other children.
>
+A tree that has properties 3, 4, and 5, but in which 1 does not necessarily hold and in which property 2 is replaced by 2a. 2a) Every leaf has a label from V ∪ T ∪ {λ}, This tree is now said to be a partial derivation tree (subtree).
+The string of symbols obtained by reading the leaves of the tree from left to right, omitting any λ’s encountered, is said to be the *yield of the tree*.


## Relation Between Sentential Forms and Derivation Trees
**Theorem 5.1:** Let G = (V, T, S, P) be a context-free grammar. Then for every w ∈ L(G), there exists a derivation tree of G whose yield is w. Conversely, the yield of any derivation tree is in L(G). Also, if tG is any partial derivation tree for G whose root is labeled S, then the yield of tG is a sentential form of G.
![[Pasted image 20250525203401.png | 350]]![[Pasted image 20250525203342.png | 350]]

## Parsing and Ambiguity
An **algorithm** that can tell us whether **w is in L(G) is a membership algorithm.** The term parsing describes finding a *sequence of productions* by which a *w ∈ L(G) is derived.*
• The grammar S → SS | aSb | bSa | ab | ba 
	• Given any w ∈ {a,b}+ , the exhaustive search parsing method will always **terminate** in no **more than |w| rounds.** 
	This is clear because the length of the sentential form grows by *at least one symbol* in each round. After *|w| rounds* we have either produced a parsing or we know that w $\epsilon$ L(G).
Round 0 is not count, we just listing out the rules 
To check if the *w* can be written based on the preliminary  
>[!Tip] Theorem 5.2:
> Suppose that **G = (V, T, S, P**) is a **context-free** grammar that **does not have** any rules of the form              **A → λ, or A → B,** 
> where A, B ∈ V.
>  Then the exhaustive search parsing method can be made into an algorithm which, for any 
>  w ∈ Σ * , either produces a parsing of w or tells us that no parsing is possible.

## s-Grammar : Simple Grammar
>[!Tip] Definition 5.4: 
>A context-free grammar G = (V, T, S, P) is said to be a **simple grammar or s-grammar** if ==all its productions== are of the form
>      *A → ax*, where A ∈ V, a ∈ T, x ∈ V* , 
> and any pair (A, a) occurs **at most once in P.**
> Example:
> ![[Pasted image 20250525205741.png]]

>[!Important] How to prove a s-Grammar
>Cond.1: G1 satisfies the form A->ax with a is one terminal, x is string of variables $\epsilon$ V
>Cond.2: (S,a) (S,b) (S,c) occur once in G1
>+ Second case:
>+ Cond1: G2 satisfies ....
>+ (S,a) occur twice in G2 --> G2 is not s-Grammar

>[!Example] 
>S --> aS | bA
>A --> aAA |b
>Cond1: Gx satisfies...
>Cond2: (S,a) (S,b) (A,a) (A,b) occurr once in G

## Ambiguity in Grammars and Languages
• Given any *w ∈ L(G)*, exhaustive search parsing will produce *a derivation tree for w.* 
• A possibility that a number of different derivation trees may exist. This situation is referred to as **ambiguity**.
--> more than 1 tree --> ambiguity (given 1 string)

>[!Tip] Definition 5.5: 
>A context-free grammar G is said to be ambiguous if there exists some *w ∈ L(G)* that has at least *two distinct derivation trees.* Alternatively, ambiguity *implies* the *existence of two or more leftmost or rightmost derivations.*

To make a Grammar unambiguous
![[Pasted image 20250526101414.png | 400]]

>[!Tip] Definition 5.6:
> If L is a context-free language for which there exists an unambiguous grammar G, then L is said to be unambiguous. If every grammar that generates L is ambiguous, then the language is called inherently ambiguous

+ One of the most *important uses* of the theory of *formal languages* is in the definition of programming languages and in the construction of *interpreters and compilers* for them
+ Both *regular and context-free languages* are used to define a programming language. While regular languages are used in the *recognition of certain simple patterns* that occur in programming languages, context-free languages are needed to model more *complicated aspects*
