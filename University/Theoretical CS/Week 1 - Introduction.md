Chapter 10 --> abort
Final 90 mins --> OPEN BOOK --> bonus point EXERCISES, ATTENDENCE | Mid term

Theoretical Computer Science : TCS
### Chapter 1 - Theory of computation --> several topics
- Automata theory
- Formal languages
- Complexity --> reference DSA 

#### Formal language theory 
- language : set of sentences (String)
- sentence: string of alphabet --> 1 sentence = string
- grammar: syntax, rules to create a statement
- production : apply rules to create string 
- deduction: from 1 variable  --> systems
- Capabilities & Limitation: Finite set of word and grammar ( condition ) since it based on computer
- Applications : apply in programming languages, specifying 1 language via FL
- TCS : can help to create and specify (syntax) a programming language.
- --> Programming languages : python, cpp, java, etc.
Note : state machine : Web
		model       : automata

#### Automata Theory : Abstract Machines
- Study a model for computing process with various resources
- It is ==computable==
- Application: parsing algorithms -> translate algorithm
- --> WEB and AI : popular topic for automata
## What is Automata ? 
- It is abstract model : not a running model, theory | not a real machine
- Compute ==automatically== the input following a set of states
- SINGULAR form : automaton : 1 abstract model to compute automatically
- Plural form : automata : multiple abstract models
- ==Applications==: AI, computational theory, compiler design parser...
	`Optimize algorithm : we can just run 1/4 the input through these model 
![[Pasted image 20250303094719.png]]
--> : initial state
Double circle : run from the "-->" to the final state
Ring: "graph" theory : go from s1 return to s1 
Transition/Move : from one state s1 to s2 
Number: "0/1" are labels

For example : 
- W1 = 10010110
- S1 (-1->) S1 (-0->) S2 (-0->) S1 (-1->) S1 (-0->) S2 (-1->) S2 (-1->) S2 (-0->) S1
A ring surrounded by another ring
	- Initial state : starts with 1 ring
	- final state : multiple ring
In the example : S1 has 2 ring --> It is the start and the end of the program.
A statement is valid <==> When it goes to the ==final step== at the end of the cycle.
==Intuitive== : it checks number of even 0s --> so odd 0s will not end up in the final state

## Formal Language
- FL is a string of words under ==specific rules / regular grammar==
- **Applications**: computer language, programming language, compiler..
- For example : below, there are **3 rules** to construct the sentence "The chef cooks the soup"
- S = NP + VP
- NP = D + N
- VP = V + NP
![[Pasted image 20250303100912.png]] 
  **Formal Languages: Review**
![[Pasted image 20250303101738.png]]
Language exponentiation: L = {0, 1} 
L$^2$ = L * L = {0, 1} * {0, 1}
    = {00, 01, 10, 11}
**Small fix** --> L$^0$ = {lamb-dah | epsilon} not e
