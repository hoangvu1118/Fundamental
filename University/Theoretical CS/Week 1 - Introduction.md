Chapter 10 --> Reference
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
- It is **abstract model** : not a running model, theory | not a real machine
- Compute ==automatically== the input following a set of states
- SINGULAR form : automaton : 1 abstract model to compute automatically
- Plural form : automata : multiple abstract models
- ==Applications==: AI, computational theory, compiler design parser...
	`Optimize algorithm : we can just run 1/4 the input through these model 
![[Pasted image 20250303094719.png]]
--> : initial state
Double circle : run from the "-->" to the final state
Ring: "graph" theory 
Transition/Move : from one state s1 to s2 
Number: "0/1" are labels

For example : 
- W1 = 10010110
- -->S1 (-1->) S1 (-0->) S2 (-0->) S1 (-1->) S1 (-0->) S2 (-1->) S2 (-1->) S2 (-0->) S1
A ring surrounded by another ring
	- Initial state : starts with 1 ring
	- final state : multiple ring
In the example : S1 has 2 ring --> It is the start and the end of the program.
A statement is valid <==> When it goes to the ==final state== at the end of the cycle.
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
Language exponentiation: L = {0, 1}  : It is form of **repeated language concatenation**
L$^2$ = L * L = {0, 1} * {0, 1}
    = {00, 01, 10, 11}
**Small fix** --> L$^0$ = {$\lambda$ | ε } not e
Empty String : **e, ε, λ or even Λ**
### Why Study Automata & Formal Language ?
- FL and Automata :
	- present theoretical aspects of CompSci
	- define infinite languages in finite way
	- construct algorithm
	- decide if a string is in language or not

Alan Turing ( 1912 - 1954 ) Father of Modern CompSci
English mathematician
--> Turing machine : abstract machines

## Fundamentals
### Language: 
A language is a collection of sentences of ==*finite length*== all constructed from a finite alphabet of symbols
### Alphabet
This is a ==finite, non-empty== set of symbols.
![[Pasted image 20250303110723.png]]

### String 
A string or word is a ==finite== sequence of symbols chosen from $\sum$
Notion: **Empty string** is $\lambda$ or (lamn-dah)
![[Pasted image 20250303111437.png]]
+ Length of a string w --> "|w|" = number of (non-lambda) characters in the string
+ e.g: w = 010100 --> |w| = 6
	+ w = $\lambda$         --> |w| = 0

- **Properties**:
	- Any string of consecutive symbols in some w is SUBSTRING of w
		- E.g: w = a1a2a3b1b2b3 then a1a2a3 & a3b1b2 are substrings of w
		- There are total of 22 substring from length 1 to length 6
- **Prefix**: 
	- The consecutive symbols at the head of the string
		- E.g,: w = uv, then u is the prefix of w 
			- --> uv is the prefix of w since after uv, the string still contains $\lambda$ (empty)
		- $\lambda$ can still a prefix of another $\lambda$
- **Suffix**:
	- Consecutive symbols at the tail of the string
		- E.g: w = uv, v is a suffix of w ~~ similar to prefix
![[Pasted image 20250303112706.png]]
==|Prefix| = |Suffix|==

- **Operators**:
	- wv is a *concatenation* of two string w and v:
		- E.g: w = a1a2a3...aN,  v = b1b2b3....bN --> wv = a1a2a3...aNb1b2b3....bN
		- $\lambda$ * w = w * $\lambda$ = w
	- Length of wv : |w * v| = |w| + |v|
+ **Reverse**
	+ It is obtained by writing symbols in reverse order and denoted by w$^R$
		+ E.g: w = a1a2a3...aN --> a$^R$ = aN...a3a2a1

- **Power** of a string (w$^n$):
	- w$^n$ : string obtained by repeating string "w" n times
		- --> w$^n$ = w.w.w...w . w (n times)
	- ==Special Case:== w$^0$ = $\lambda$ for all w
![[Pasted image 20250303113838.png]]
 For example:
	- Z = {0, 1, 2}
	--> $\sum^3$ = {012, 000, 111, 222, 120, ...}
	 --> $\sum^*$ = {$\lambda$ , 0 ,1, 2, 01, 02, 12, 00, 011, ... }
	 --> $\sum^+$ = {0, 1, 2, 01, .....}

Sigma (+) & ( * ) : always **INFINITE** since there is no LIMIT on length of the string
However, when being used in computer --> it becomes finite.
## Language
##### Definition: 
- A language **L** is defined generally as a SUBSET of $\sum^*$ 
- a String in a language L is called **sentence** of L
![[Pasted image 20250303114605.png]]
 $a^n$ $b^n$ is lambda when n = 0 
#### Operations
+ Complement of a language L: 
	+ $\neg{L}$ = $\sum^*$  - L
+ The reverse of a language $L^R$ is the set of all string reversals:
	+ $L^R$ = {$w^R$ : w belongs to L}
+ The concatenation of two languages L1 and L2 denoted by $L_{1}L_{2}$ :
	+ $L_{1}L_{2}$  = {xy : x $\epsilon$ L1, y $\epsilon$  L2}
+ $L^n$ as L concatenated with itself n times 
	+ L = {$a^nb^n$ | n >= 0} then $L^2$ = {$a^nb^na^mb^m$ | n>=0, m >= 0}
	+ $L^0$ = $\phi$ = {$\lambda$}
	+ $L^1$ = L
![[Pasted image 20250303115454.png]]

```Text
Summary:
- Formal language theory: 
	- alphabet is set of finite, NON-empty set of Symbols
	- language is set of sentences (string)
	- sentence is string of alphabet : 1 sentence = 1 string
- Automata :
	- It is an abstract model : not realistic running model 
	- A mathematical model which is able to regconize pattern, processing input based of predefined rules (set of instructions)

- Formal Language: 
	- string that is constructed by a set of rules (grammar / components / article)
	- string has multiple operations/ traits
		- prefix/suffix elements will be the same --> it is the order that matter
		- reverse : set of symbols in reverse order
		- power: string obtained by repeating n times
		- Sigma(n) : set of all string of lengths n
		- Sigma(*) : set of strings include lambda, zero and other symbols
			- always contain lambda
		- Sigma(+) : set of strings that exclude lambda
	- Sigma is finite by ASSUMPTION , + & * are infinite 
	- However, when apply on computer --> all infinite
- Language is a subset of ALPHABET(sigma*)
```
