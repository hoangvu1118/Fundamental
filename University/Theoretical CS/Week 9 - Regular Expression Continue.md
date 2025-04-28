![[Pasted image 20250428092457.png | 400]]

### To convert a regular expression to nfa, we use
A *rectangle* -> is a NFA
![[Pasted image 20250428092535.png | 400]]
*STEP 1*: These are *primitive reg expression*
We fractorize 'em' out -> then we can draw a NFA for it

*Step 2*: Build up nfas by *the complex regular expression*:
r1 + r2
![[Pasted image 20250428093554.png | 450]]
    
![[Pasted image 20250428094014.png | 400]]
A NFA for regular expression r*
![[Pasted image 20250428094128.png | 400]]
**EXAMPLE PROBLEM**
![[Pasted image 20250428151034.png | 700]]
![[Pasted image 20250428151106.png | 500]]

## Generalized Transition Graph (GTG)
• A *generalized transition graph (GTG)* is a transition graph whose edges are labeled with regular expressions; otherwise, it is the same as the usual transition graph. 
• The label of any walk from the initial state to a final state is the concatenation of several regular expressions, and hence itself a regular expression. 
• The strings denoted by such regular expressions are a subset of the language accepted by the GTG, with the full language being the union of all such generated subsets.

GTG is a representation of a NFA
*Example: GTG*
![[Pasted image 20250428114144.png | 350]]

The *graph of any nfa can be considered a GTG* if the *edge labels* are interpreted *properly*. 
• An edge labeled with a single symbol a is interpreted as an edge labeled with the expression a. 
• An edge labeled with multiple symbols a, b,…is interpreted as an edge labeled with the expression a + b + ….

For every *regular language*, there exists a GTG that accepts it. 
Conversely, *every language* accepted by a *GTG is regular.* 
• Since the label of every walk in a GTG is a regular expression, this appears to be an immediate consequence of Theorem 3.1

• To find a regular expression for a GTG, we need to remove the intermediate states to the simplest equivalent GTG. 
• *Immediate states*: are neither initial states nor final states
![[Pasted image 20250428114457.png | 450]]


