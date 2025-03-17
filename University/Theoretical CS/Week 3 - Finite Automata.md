## 0. Applications: Not for automata - But languages
Provided the basic knowledge to build the programming languages, compiler
+ Grammar is used to **define the programming languages**
+ Accepter is used to **define some of parts of the programming languages**
+ Build the lexical analyzer and syntax analyzer for programming languages.

## 1. Deterministic Finite Accepters (DFA)
>[!Definition] 
>A dfa is defined by the quintuple
![[Pasted image 20250317094553.png]]

F is subset of Q and it contains final states
Red: current state + input --> output the next state
For automata case, internal state can cover initial and final state

**DFA Operation** ~ similar to input mechanism in automata (lecture 1)
+ At the ==initial time==, it is assumed to be in the initial state q0, with its input mechanism on the *leftmost symbol of the input string.* 
+ The input mechanism can move *only from left to right* of the input string and *reads exactly one symbol on each step*
Since it is a Accepters --> a type of automa