## 0. Applications: Not for automata - But languages
Provided the basic knowledge to build the programming languages, compiler
+ Grammar is used to **define the programming languages**
+ Accepter is used to **define some of parts of the programming languages**
+ Build the lexical analyzer and syntax analyzer for programming languages.

## 1. Deterministic Finite Accepters (DFA)
>[!Definition] 
>A dfa is defined by the quintuple
![[Pasted image 20250317094553.png | 400]]

is a finite-state machine that *accepts or rejects* strings of symbols, *transitioning to a unique next state based* on the current state and input symbol, making the computation path deterministic

F is subset of Q and it contains final states
Red: current state + input --> output the next state
For automata case, internal state can cover initial and final state

**DFA Operation** ~ similar to input mechanism in automata (lecture 1)
+ At the ==initial time==, it is assumed to be in the initial state q0, with its input mechanism on the *leftmost symbol of the input string.* 
+ The input mechanism can move *only from left to right* of the input string and *reads exactly one symbol on each step*
+ During each move of the automaton, the input mechanism advances *one position to the right*, so each moves consumes one input symbol

**MIGHT be in the Midterm**
Since it is a Accepters --> a type of automata --> so its has same rules and grammar to automata in lecture 1
> [!Warning]
> When the end of the string is reached, the string is *accepted* if the automaton is in one of its final states. Otherwise, the string is *rejected*

![[Pasted image 20250317095801.png]]

**TRANSITION GRAPH** : To *visualize* and *represent* finite automata
![[Pasted image 20250317095948.png]]
> [!example] 
> ![[Pasted image 20250317100043.png ]]

--> Basically we make a GRAPH by those transition function $\delta$ 
To determine if is valid DFAe
--> Check if at each state --> does it have at least the length $\sum$ outgoing (from that state go out to other state) function from that state --> in the example --> length of $\sum$ is 2

> [!example]
> w1 = 100
> $\delta$(q0, 1) = q1 (4)
> $\delta$(q1, 0) = q0 (2)
> $\delta$(q0,0) = q0 (1)
> --> Rejected since q0 is not a subset of F
> w1 = 100 is REJECTED by F via a sequence of rules (4,2,X)
> 
> w2 = 101
> $\delta$(q0, 1) = q1 (4)
> $\delta$(q1, 0) = q0 (2)
> $\delta$(q0, 1) = q1 (4)
> --> Accepted since q1 is a subset of F
> w2 = 101 is ACCEPTED by F via a sequence of rules (4,2,4)
> 
> w3 = 0001
> $\delta$(q0, 0) = q0 (1)
> $\delta$(q0, 0) = q0 (1)
> $\delta$(q0, 0) = q0 (1)
> $\delta$(q0, 1) = q1 (4)
> --> Accepted since q1 is a subset of F
> w3 = 0001 is REJECTED by F via a sequence of rules (1,1,1,4)
> 
> w4 = 0111
> $\delta$(q0, 0) = q0 (1)
> $\delta$(q0, 1) = q1 (4)
> $\delta$(q1, 1) = q2 (5)
> $\delta$(q2, 1) = q1 (6)
> --> Accepted since q1 is a subset of F
> w4 = 0111 is ACCCEPTED  by F via a sequence of rules (1,4,5,6)
> 
> Since time is not enough --> I only write the final statement for the rest
> w5 = 1100
> w5 is REJECTED by F via a sequence of rules (4,5,3,X)
>
> w6 = 01001
> w6 is ACCEPTED by F via a sequence of rules (1,4,2,1,4)
> 
> w7 = 11001
> w7 is ACCEPTED by F via a sequence of rules (4,5,3,3,6)
> 
> w8 = 0000110
> w8 is REJECTED by F via a sequence of rules (1,1,1,1,4,5,3)
> 1,1,1,1,4,5,3

**Extended Transition function**
$\delta$* : Q x $\sum$* --> Q
- The 2nd argument of $\delta$* is *a string*, rather than a single symbol
-  $\delta$* 's value gives the state the automaton will be in after reading that string
> If $\delta$(q0, $\alpha$) = q1, $\delta$(q1, b) = q2
> Then --> $\delta$* (q0, ab) = q2
> --> $\delta$* (q0, 0001) = q1

>$\delta$* is defined recursively by:
>$\delta$* (q, $\lambda$) = q, --> assume that lambda is a string of multiple lambda
>--> in some case we can remove that "asterisk(* )"
>![[Pasted image 20250317111117.png]]
-> w is a string of vb --> with b is the right most --> recursively split the string except the rightmost
--> we end up with the result at the left most

**Associated Language of DFA's**
>[!Definition] Def 2.2:
>The language L accepted by a dfa M = (Q, $\sum$, $\delta$, q0, F) is set of all strings on $\sum$ accepted by M

>--> Formal Notation: L(M) : { w $\epsilon$ $\sum$* : $\delta$* (q0, w) $\epsilon$ F}
>
![[Pasted image 20250317111643.png]]

**EXAMPLE**
![[Pasted image 20250317111718.png]]
The language L accepted by the automaton is *L(M) = {a$^n$ b : n $\ge$ 0}*

**Trap state:** when the dfa goes into trap state from which it can never escape. 
• E.g., q 2 is the trap state. 
• Trap state can be the last state or not. (not final) --> reject
• Can be defined for the trap state group which can be final or not.

**TRANSITION TABLE**
![[Pasted image 20250317112941.png]]

>[!warning]
>Since it is DFA (deterministic finite automata) --> each outgoing edges have to be unique 
>otherwise the rules will be violated 

**Regular language**
>[!Definition]
>A language is called **regular** if and only if there exists some deterministic finite accepter (dfa) M such that L = L(M)
>![[Pasted image 20250324093517.png | 400]]
 
## Nondeterministic Finite Accepters (NFA)
>[!Def]
>It is defined by the quintuple
>**M = (Q, $\sum$, $\delta$, q0, F)**
>
>![[Pasted image 20250324105821.png]]

**The range of $\delta$ is in the power set 2$^Q$ so that its value is not a single element of Q but a ==subset== of Q**
--> Subset is defined as the set of all possible states that can be reached by the transition
![[Pasted image 20250324111017.png]]

 **.$\lambda$ is allowed to be the second argument of $\delta$**
 + This means that nfa can make a transition **without** consuming an input symbol
 + Although we still assume that the input mechanism can **only** travel to the **right**, it is possible that it is ***stationary*** on some moves
 ![[Pasted image 20250324111331.png]]
 --> This is slight difference from the **TRAP** method 
 --> This results in an empty set --> which can still be used (the machine stops and union/combine this result with other result)
**NFA can be represented by a *transition graph*** 
![[Pasted image 20250324111959.png | 450]]

**Similarity**
NFA and DFA are both defined by a quintuple M = **M = (Q,$\sum$, $\delta$ , q0, F)** (5 components)
NFA and DFA move based on input symbols from the alphabet $\sum$ 
They use transition diagram to display changes between states

**Difference**

| NFA                                                                                                                            | DFA                                                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| + Each edge can have multiple similar label going out from one state \| for example q0 can have 2 paths with labels a          | + Each states have unique outgoing edges (a and b for example)                                                                                                                  |
| + Each state can have multiple outgoing edges or can even have empty edge \| arrow (which mean at that state it is stationary) | + Each state have at most at and at least the number of edges similar to the number of component in the alphabet (for example $\sum$ ={a,b} so each edge have two path a and b) |
| + A state in NFA can have a lambda path which signify the dead configuration                                                   | + DFA do not support this, each output have to have a label from the input symbols                                                                                              |
| + It returns set of states 2$^Q$                                                                                               | + It returns one state                                                                                                                                                          |

**Extended Transition Function**

It is defined as **.$\delta$ * (qi, w)** 