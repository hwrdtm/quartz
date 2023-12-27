---
title: "Mathematics Background"
---

# Sets and Groups

Sets are just a collection of objects. 

A Cartesian product of two sets is a new set that is constructed from the two sets. The Cartesian product between sets $A$ and $B$ is denoted by $A \times B$ .
- Let $A = \{1, 2\}$ and $B = \{3, 4 \}$ then $A \times B = (1,3), (1,4), (2,3), (2,4)$ 

A pair $(G, \bullet)$ consisting of a set $G$ and a binary option $\bullet : G \times G \rightarrow G$  is a commutative (abelian) group if it satifies the following properties:
- Identity 
- Inverses
- Associativity
- Commutativity

An operation is closed if the result is also in the same set as the elements input to the operation.

Examples of groups
- $(\mathbb{Z}, +)$ is a group where $\mathbb{Z}$ is the set of integers
	- The identity element of the set $\mathbb{Z}$ of integers with respect to addition is $0$ .
- $(\mathbb{N},\cdot)$  is NOT a group where $\mathbb{N}$ is the set of natural numbers
	- The identity element of the set $\mathbb{N}$ of natural numbers with respect to multiplication is $1$.
	- $2$ does not have a multiplicative inverse in $\mathbb{N}$ , for example.
	- Since no inverses, not a group.
- $(\mathbb{Z}_{7}, \otimes)$ is not a group because $0$ does not have an inverse.
- $(\mathbb{Z}^{\otimes}_{7}, \otimes)$ is a group where $\mathbb{Z}^{\otimes}_{7}$ is $\mathbb{Z}_{7}$ excluding $0$, or $\mathbb{Z}^{\otimes}_{7} = \{1,2,3,4,5,6\}$ .

Let $n \in \mathbb{N}$ and $\mathbb{Z}_{n} = \{0,1,2,...,n-1\}$ , we define two binary operations $\oplus$ and $\otimes$ as:
- Addition Modulo: $\oplus : \mathbb{Z}_{n} \times \mathbb{Z}_{n} \rightarrow \mathbb{Z}_{n}, a \oplus b \coloneqq (a + b) \bmod n$ 
- Multiplication Module: $\otimes : \mathbb{Z}_{n} \times \mathbb{Z}_{n} \rightarrow \mathbb{Z}_{n}, a \otimes b \coloneqq (a \cdot b) \bmod n$ 

# Powers and Logarithms

Exponentiation is repeated multiplication.

The exponentiation notation for group elements is defined as repeated application of the group operation.
- To be able to distinguish exponentiation with respect to different binary operations in our notation of powers of group elements we always give the binary operation next to the exponent.

Group exponentiation
- Let $(G,\star)$ be a group and $b \in G$
- For $n \in \mathbb{N}$ we set $b^{n\star} = b \star b\ \star \ ... \ \star \ b$ ($b$ goes through the $\star$ operation $n$ times)
- We set $b^{0\star} = e$ where $e \in G$ is the identity of the group $(G,\star)$

Two approaches for computing $6^{8\otimes}$ in the group $(\mathbb{Z}^{\otimes}_{11}, \otimes)$  where $a \otimes b = (a \cdot b) \bmod 11$ 
1. Naive Exponentiation: We repeatedly apply $a \otimes b = (a \cdot b) \bmod 11$ eg. first compute $6 \otimes 6 = (6 \cdot 6) \bmod 11 = 36 \bmod 11 = 3$ and then so on.
2. We compute $6^{8}$ in the integers and compute the result $\bmod 11$ , eg. $1679616 \bmod 11 = 4$.

2nd approach is infeasible with larger bases and exponents.

Strategies for efficient computation
- Repeated squaring: Used to compute $b^{2a}$ when $b^{a}$ is known.
- [Fast exponentation](https://mathstats.uncg.edu/sites/pauli/112/HTML/secfastexp.html): Is a generalization of the Repeated Squaring strategy above for any power.

Discrete Logarithm Problem
- The discrete logarithm to the base $b$ of $a$ is the answer to the question: given $a$ and $b$, what is the (smallest) non-negative integer $m$ such that $a = b^{m\star}$?
- The discrete log $m = log^{\star}_{b} a$ does not always exist.
- Complexity of calculating the discrete log of any arbitrary number in a large group is high.

Many algorithms exist to efficiently (attempt) to find the discrete log.

Powers in $(\mathbb{Z}^{\otimes}_{7}, \otimes)$:
- powers of 1 are $1^{0\otimes} = 1^{1\otimes} = ... = 1$
- powers of 2 are $2^{0\otimes} = 1, 2^{1\otimes} = 2, 2^{2\otimes} = 4$ where we continue to cycle through numbers 1, 2, 4.
- powers of 3 are $3^{0\otimes} = 1, 3^{1\otimes} = 3, 3^{2\otimes} = 2$ where we enumerate through all the numbers 1, 2, 3, 4, 5, 6, which means all elements of $\mathbb{Z}^{\otimes}_{7}$ are powers of 3.
- ...similar for powers of 4, 5, 6.

Exponentiation and discrete logarithm to the same base are inverse functions.

# Public Key Cryptography

Diffie Hellman Key Exchange
1. First Alice and Bob agree on the group they will work in. Subsequently, all computations will take place in group $(\mathbb{Z}^{\otimes}_{p}, \otimes)$ where $a \otimes b = (a \cdot b) \bmod p$
	- Alice and Bob agree on a prime number $p$ and generator $g \in \mathbb{Z}^{\otimes}_{p}$ over insecure channel
2. Alice then chooses her secret $a \in \mathbb{N}$ and computes $A = g^{a\otimes} = (g^{a}) \bmod p$ and sends $A$ to Bob.
	- Recall the proof here: https://mathstats.uncg.edu/sites/pauli/112/HTML/secmod.html#theomultmod
3. Bob chooses his secret $b \in \mathbb{N}$ and computes $B = g^{b\otimes} = (g^{b}) \bmod p$ and sends $B$ to Alice.
4. Alice computes the shared secret $s_{A} = B^{a\otimes} = (B^{a}) \bmod p$
5. Bob computes the shared secret $s_{B} = A^{b\otimes} = (A^{b}) \bmod p$
6. The shared secrets are the same $s_{A} = B^{a\otimes} = (g^{b\otimes})^{a\otimes} = g^{(a \cdot b)\otimes} =(g^{a\otimes})^{b\otimes} = A^{b\otimes} = s_{B}$

Assume someone eavesdrops on channel and obtains $p$, $g$, $A$ and $B$. To obtain the secret, the attacker needs either $a$ or $b$ which **can only be found by finding the discrete logarithm of $A$ to base $g$ in $(\mathbb{Z}^{\otimes}_{p}, \otimes)$** or vice versa for $B$ - the security of the protocol depends on the difficulty of computing discrete logarithms in $(\mathbb{Z}^{\otimes}_{p}, \otimes)$.
- The difficulty in finding the discrete logarithm depends on how large the $p$ prime number is.

# Fields

Let $\mathbb{R}$ be the real field, $\mathbb{C}$ the complex field, $\mathbb{Q}$ the field of rational numbers, and $\mathbb{F}_{2}$ the binary field.

A field is a set $\mathbb{F}$ of at least two elements with two operations $\oplus$ and $\otimes$ which satisfies the following properties:
- $(\mathbb{F}, \oplus)$ is an abelian group with an identity element $0$.
- $(\mathbb{F} - \{ 0 \}, \otimes)$ is an abelian group with an identity element $1$
- Distributive law: $\forall a, b, c \in \mathbb{F}, (a \oplus b) \otimes c = (a \otimes c) \oplus (b \otimes c)$

A finite field (aka Galois field) is a field with a finite number of elements.

Examples
- $\mathbb{R}$, $\mathbb{C}$, $\mathbb{Q}$ and $\mathbb{Z}_{p}$ where $p$ is prime are all fields with the usual operations $\oplus$ and $\otimes$.
	- Note that $\mathbb{Z}_{p}$ where $p$ is prime can also be denoted as $\mathbb{F}_{p}$ . It has the set of elements $R_{p} = \{ 0, 1, ..., p -1 \}$ and is an example of a finite (Galois) field. 
	- Another notation of the above is GF($p$) and is called the prime field of order $p$.

# Polynomials

Polynomials over $\mathbb{F}_{p}$ are polynomials whose coefficients lie in $\mathbb{F}_{p}$ and for which polynomial addition and multiplication is performed in $\mathbb{F}_{p}$.
- The rules for adding, subtracting, or multiplying polynomials are the same over a general field $\mathbb{F}$ as over the real field $\mathbb{R}$ except that the coefficient operations are in $\mathbb{F}$.

The set of all polynomials over $\mathbb{F}$ in an indeterminate $x$ is denoted by $\mathbb{F}[x]$.
- This set has many of the properties of a field, eg. it is an abelian group under addition whose identity is the zero polynomial $0 \in \mathbb{F}[x]$ . It has a mulplicative identity $1 \in \mathbb{F}[x]$ and the distributive law holds.


# Resources

https://mathstats.uncg.edu/sites/pauli/112/HTML/secsetdef.html
https://mathstats.uncg.edu/sites/pauli/112/HTML/chaptergroups.html
https://en.wikibooks.org/wiki/LaTeX/Mathematics
https://web.stanford.edu/~marykw/classes/CS250_W19/readings/Forney_Introduction_to_Finite_Fields.pdf
http://math.ucdenver.edu/~wcherowi/courses/m6406/finflds.pdf
https://mathworld.wolfram.com/FiniteField.html