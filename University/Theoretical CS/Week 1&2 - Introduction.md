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
- Read for rules further below for *clarification*
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
	- Length of wv : |wv| = |w| + |v|
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

## Mathematical Preliminaries and Notation
- Set with no elements --> empty set or the null set ==> $\phi$

## Mid-term test 
30 multiple choices question covering lesson 1 
Some writing ... lesson 2
==> OPEN Book

### Grammar 
- Powerful tools for *describing* and *analyzing* languages
- Set of rules by which **valid** sentences in a language are constructed
- string : sentence in grammar
Ex: `<sentence> -> <noun phrase> <predicate>` "predicate " : verb --> 1
 `<noun phrase> -> <article> <noun>` --> 1
 `<predicate> -> <verb>` --> 1
 `<article> -> a | the` --> 2
 `<noun> -> boy|dog` --> 2
 `<verb> -> run|walk` --> 2
--> Here we have 9 rules to construct a sentence
`Note: Pay attention to the sign or ("|") --> each element will be a rule`

- The sentence "a boy runs" and "the dog walks" are properly formed
- If we were given a complete grammar, then in theory, every **proper** sentence could be *explained*
==`Definition 1: A Grammar G is defined as a quadruple`==
**G = (V,T,S,P)**
**Notion:**
*V* : finite set of objects call *variables* (nonterminal symbols)
*T*: is a finite set of objects called *terminal symbols*
*S* $\epsilon$ V : special symbol called *start variable*
*P* : finite set of production ( means rules --> create a sentence)

Terminal : cant not replace with any variable | values since it is a final value
Terminal : constant
Non-terminal : variable

**Notation**
- A,B,C ... Uppercase: variables --> S : start variable
- a, b, c, d, e, digits, strings: terminal ( symbols such as "h", "e", "l" , "l")
- X, Y, Z : variables or terminals
- u, v ,w, x ,y ,z : string of terminals --> ex: "Hello World" -> It holds multiple terminals
- α,  β,  γ,  δ : string of variables and terminals --> this is a mix 
- String of variables : X = ABF --> A can be a, b, c 
- X is only variables or only terminals OR even both
- Consider we use "u" for string of terminal and A for a variable "a"
- --> α = uA
 **Sentential Form: a string that still hold variable --> can still process, not reach the terminal yet** --> contain both variables and terminals
 
**Production**
- A production has the form **x -> y**
	- where **x** is a element of ( V $\cup$ T )$^+$ and **y** is in (V $\cup$ T)$^*$ 
	- (V u T)$^+$  = {aA, ab, AB, aab, AA, .....}
	- (V u T)$^*$ = {aA, ab, AB, aab, AA, .....} u {$\lambda$}
		- V = {A, B, E, F}
		- T = {a, b, c, d}
		--> AbDcd $\epsilon$ (V $\bigcup$ T)$^+$  x # $\lambda$ 
- **Production** has another name *rule* or *written rule*
- According to the grammar G = {V,T,S,P}
- G = ( {S,A,B}, {a,b} , S, P), with P:
	 - S -> aAS | bBS | $\lambda$,
	 - A -> aaA | b,
	 - B -> bbB | a,
- Must start from S, then we can construct a sentence from other variable S, A, B 
- We can end when reach the final (terminal) form

**Deriving Rule**
Given a string w of the form : **w = uxv**
- Apply the production rule *x->y* to the string w, by replacing x with y, then obtain a new string *z = uyv*
- So, *w => z* or *uxv => uyv* ( say that w *derives* z or that z *is* *derived* from w)
![[Pasted image 20250310100215.png]]

==`Definition 2 : Let G = {V, T, S , P} be a grammar`==
Then the set L(G) = {w $\epsilon$ T$^*$ , S =$^*$> w} is the language generated by G
**Derivation** : If w $\epsilon$ L(G) then the sequence 
- S => w1 => w2 ... => wn => **w** 
	- is a derivation of the sentence w

*Example:* G  = ( {S}, {a, b} , S, P) with 
- P:
	- S -> aSb | $\lambda$ 

then S => aSb => aaSb ==> aabb is a derivation of sentence *aabb* 
So it can be rewritten as **S =$^*$> aabb**
- aabb is a sentence in the language generated by G
- aSb, aaSbb are *sentential forms*
- The language L of the grammar G is L(G) = {a$^n$ b$^n$  : n >= 0}
- L(G)  = {$\lambda$, ab, aabb, aaabbb, aaaabbbbb, ....}

## Automata 
- *Abstract model* of a real computer 
	- Operate automatically w/o human control
 - Has *rules* based on which people make programs embedded in the machine to serve their purposes (Start from S --> start deriving and get the final desired result)
- Compute some operator and (it has) small memory
Automaton has 4 components:
![[Pasted image 20250310104838.png]]
- 2 Type 
	- one with storage : in lecture 7
	- one w/o storage 

**INPUT FILE**
- Is a sequence over a given alphabet
- Is divided into cells, each of which can hold *one* symbol
- Can be read *but* cannot be changed ~~ ROM 
**INPUT Mechanism**
- Can read the input file from left to right, ==one symbol== at a time
- Can detect the end of input string (by sensing an end-of-file condition, i.e EOF or #)
**STORAGE**
- Consists of an *unlimited number of cells,* each capable of holding a single symbol from an alphabet( not necessarily the same one as input alphabet)
- The automaton *can read and change* contents of the storage cells ~ RAM
**Control Unit**
- An automaton has a control unit
- Can be in any one of a finite number of internal states
- Can change state in some defined manner
--> **Internal State**
For example: S1 --> S2 --> S3 with s1 and s3 can be either initial or final state
--> S2 will be internal state --> not start or end
This state will go with input/output

==Configurations==: go with input/output and a state Si with i $\in$(0,n)
- refers to a specific state of the automaton at a given point in time. It includes the *current state* of the *control unit*, the *input* being processed, and the *contents of any temporary storage.*
```Text
Suppose we have a simple finite automaton that reads binary strings and accepts those that end with "01". A configuration might look like this:

- *Current State: q1​ (indicating the automaton is in state q1q1​)
- *Input*: "101" (the input string being processed)
- **Temporary Storage**: None (if the automaton doesn't use additional storage)

As the automaton processes the input "101", it transitions through different states, and each combination of state and input position represents a configuration.
```
**OUTPUT**
- The automaton can produce output of some form
	- Example : one variable or sentential form

***CONCEPTS***
- *Internal State* : IT is not current state --> read the above in [Control Unit]
-  *Next Stage* : Following state of a control unit at the next time step
- *Transition function* : Gives the ==Next state== in terms of "<font color="#f79646">*the current state, the current input symbol, information currently in the temporary storage</font>"* (top of the storage) - Last in First out
	- Example: f(qi, xi, z) = {q1, q2, q3, ..}
		- qi : current state
		- xi : current input symbol
		- z : value on top of the memory
	- Automata will help to transmit data from qi to q1 | q2 | q3 (next state)with data from the current state
 -  Move :  Is the transition of the automaton from one configuration to the next one

### OPERATION
- An automaton operates in a discrete timeframe
- At any time, the control unit is in some internal state, and the input mechanism is scanning a particular symbol on the input file

- The internal state of the control unit at the next time step is determined *by the next-state or transition function* --> if we cannot find the transition function 
	- We say it go to death-end since it cant move anymore | find a death-end

- During the transition from one time interval to the next, output maybe produced or the information in the temporary storage changed

**Deterministic Automaton**
- Each move is **uniquely determined** by the *current configuration*
- If we know the internal state, the input, and the contents of the temporary storage, we can predict the future behavior of the automaton exactly
Example: f(qi, xi, z) = {q1} --> it go directly to the q1 state

**Nondeterministic Automaton**
- At each point, a nondeterministic automaton may have several possible moves, so we can only predict a set of possible actions
Example: f(qi, xi, z) = {q1, q2, q3,...) --> a set of possible states

**Accepter** 
- Is an automaton whose *output* response is limited to a simple "yes" or "no"
- With an input string, an accepter either accepts the string("yes") or rejects it ("no")
**Transducer**:
- Producing strings of symbols as output
- Computer is a typical transducer
- Type of automaton that processes an input and produces an output
	- **Speech Processing**: Converts audio signals to text.
	- **Moore Machine** : A transducer where the output depends only on the **current state** (not the input).
	- Example: A traffic light controller that changes based on a timer.

- A transducer where the output depends only on the **current state** (not the input).
- Example: A traffic light controller that changes based on a timer.
### Applications:
- Grammar  : used to define the programming languages
- Accepter: define some parts of the programming  languages - valid or invalid
- Build the lexical analyzer and the syntax analyzer for programming languages.

EXAMPLE:
![[Pasted image 20250310113839.png]]

![[Pasted image 20250310114227.png]]
3 is wrong --> should only 1 ring --> so that when the invalid syntax go into it --> return false. Otherwise, it true --> since 2 rings -> true
::=  means -> (a rule)
![[Pasted image 20250310114237.png]]
![[Pasted image 20250310115133.png]]
HOMEWORK : create ID for C
``` Text
<id> -> <letter> <rest> | <underscore> <rest>
<rest> -> <digit> <rest> | <letter> <rest> |λ,
<letter> -> a....z | A....Z,
<digit> -> 0.....9,
<underscore> -> _,
```
