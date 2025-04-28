## Regular Expression
A language is regular if there exists *a finite accepter for it*. Therefore, *every regular language* can be described by *some dfa or some nfa.*

In many instances, we need *more concise ways* of describing regular languages. The other ways of representing regular languages are named *regular expression* and *regular grammar*
--> Use formular to describe a language

>[!Definition]
>Is a combination of strings of symbols from some alphabet $\sum$ , ( ), and operators *+*, *.*, *
>We use · for concatenation, and ** for star-closure, and the + for union.
>+ The simplest case is the language {a}, denoted by the regular expression a
>+ Slightly more complicated is the language {a, b, c}, for which, we have the regular expression *a+b+c*
>+ The expression (a+(b·c))*  stands for the star-closure of {a}∪{bc}, that is, the language {λ, a, bc, aa, abc, bca, bcbc, aaa, aabc, …}

### Definition 3.1
![[Pasted image 20250421111511.png]]
*Remember these colorful text* 
Red : primitive 
Green: basic

**For example**
```Text
For Σ = {a, b, c}, the string (a+b+c) * .(c+Ø) is a regular expression since it is constructed by application of the above rules

If we take r1 = c and r2 = Ø, we find that c + Ø and (c + Ø) are also regular expressions. Repeating this, we eventually generate the whole string.
So if the string is 
	(a+b+c)+ .(c + Ø) is wrong, since there is no "+" closure

On the other hand, (a + b +) is not a regular expression, since there is no way it can be constructed from the primitive regular expressions
```

### Definition 3.2
![[Pasted image 20250421112535.png]]

If r1 and r2 are *regular expressions* then
1. L(r1 + r2) = L(r1) $\cup$ L(r2)
2. L(r1 . r2) = L(r1) . L(r2)
3. L((r1)) = L(r1)
4. L(r1*) = (L(r1))*
For the ==star closure==, it is **zero or more repetitions** of the preceding element (character, group, or pattern).
Example : (aa)* = {$\lambda$, aa, aaaa, aaaaaa, .....} it repeat the thing inside the bracket

**Priority** on the operators from *left to right*: * , ., +
The symbol for concatenation may be omitted, so we can write r1 .r2.
![[Pasted image 20250421113148.png | 500]]

>[!Example] 
>Find a regular expression for the language L = {w ∈{0,1} * : w has no pair of consecutive zeros}
>![[Pasted image 20250421114201.png | 300]]
>
>Equivalence of regular expressions: the two regular expressions are equivalent if they *denote the same language*

>[!Warning] Attention
>![[Pasted image 20250421114429.png | 200]]






