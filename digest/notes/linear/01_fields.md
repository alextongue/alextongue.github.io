---
title: "1: Fields, Vector Fields"
parent: Linear Algebra
grand_parent: Notes
nav_order: 1
layout: default
date: 2020-01-24
---

# Fields
A **field** $\mathbb{F}$ shall be a set of elements that has two specific operators defined for that set. Think of operators as black boxes that output something based on an input[^1].

The two operators that must be defined for a field will be called the additive and multiplicative operators. They can be denoted respectively as:

- $+:\mathbb{F}\times \mathbb{F} \rightarrow \mathbb{F}$
- $* : \mathbb{F} \times \mathbb{F} \rightarrow \mathbb{F}$


Reminder: we haven't defined what these "addition" and "multiplication" are yet, so bear with me if this seems slow.

For a field to exist, these operations must follow five distinct properties, the first four being as follows for $a,b,c,d\in\mathbb{F}$:

|   |Additive| Multiplicative|
|---|:------:|:-------------:|
|**Associativity** | $(a+b)+c=a+(b+c)$ | $(a \cdot b)\cdot c = a \cdot(b \cdot c)$ |
|**Commutativity** | $a+b=b+a$ | $a \cdot b = b \cdot a$ |
|**Identity Element** | $a+0=a$ | $a \cdot 1 = a$ |
|**Inverse Element** | $a+(-a)=0$ | $a \cdot a^{-1}=1, a\neq0$ |

> The nice part, is that "scalar addition" and "scalar multiplication" adhere to these properties!

Sometimes, the term "Abelian group" will be used to discuss the constituent parts of a field. Each single operation that adheres to the above four properties and is defined over the field, shall be called an **Abelian group**. When the field $\mathbb{F}$ is paired with the additive and multiplicative single operations separately, the resulting groups $(\mathbb{F}, +)$ and $(\mathbb{F}\setminus\{0\} , \cdot)$[^2] form Abelian fields.

Finally, the fifth property links the two operations together (thus linking the two Abelian groups discussed above):

|   | Addition, Multiplication $(+,*)$ |
|:--|:--------------------------------:|
|**Distributivity**| $a \cdot (b+c) = a \cdot b + a \cdot c$|

It is worth knowing that that Abelian groups are closed under their operation:

- For group $(\mathbb{F},+)$, $a+b \in \mathbb{F}$. 
- For group $(\mathbb{F},*)$, $a \cdot b \in \mathbb{F}$.

It follows then, that the field $(\mathbb{F},+,*)$, is closed under both operations. Any combination of elements in $\mathbb{F}$ using operators $+$ and $ * $ will yield a result that is still in $\mathbb{F}$.

**In summary:** If a set of numbers is closed under two operations that each have an associative property, a commutative property, an identity element, and an inverse element, and the operations are related through the distributive property, then it is a field.

## Final Note: The Real Field

Fields can be thought of as primitive number types on which more complex principles of linear algebra are built. So far, we have used the general notation of fields, $\mathbb{F}$. Examples of other specific fields include:

- $\mathbb{R}$: The set of real numbers
- $\mathbb{Z}$: The set of integers (e.g. $-37,1,2,3, 100$)
- $\mathbb{Z}_p$: Only the set of integers that exist as a remainder of division by p (modulo p) (e.g. $\mathbb{Z}_3 = \{0,1,2\}$)
- $\mathbb{C}$: The set of complex numbers $\begin{Bmatrix} X \mid X = \sigma + j\omega : \sigma,\omega\in\mathbb{R};\; j=\sqrt{-1} \end{Bmatrix}$

For most of the definitons, we will use the field $\mathbb{R}$. In virtually all other cases, the definitions and proofs over field $\mathbb{R}$ still hold when proven over other fields.

# Vector Fields

Elements in the real field $\mathbb{R}$ can be used to build  collections of real numbers and treated as elements themselves. These shall be called **vectors**. For example, for $r_1,r_2,r_3, r_4\in\mathbb{R}$, the following are considered vectors:

$$\begin{pmatrix} r_1 \\ r_2 \end{pmatrix}, \begin{pmatrix} r_1 \\ r_2 \\ r_3\end{pmatrix}, \begin{pmatrix} r_1 & r_2\\ r_3 & r_4 \end{pmatrix}$$

> Although it might seem intuitive and straightforward to call these something along the lines of a "field of a field" or "nested field" and extrapolate the same five properties used in defining a field, they must be regarded as different creatures altogether, with explicit definitions of its necessary operations.

Then, we shall define **vector addition** as the addition of its constituent field elements. For vectors with $p$ different elements per vector, $A=[a_1, a_2, \cdots, a_p], B=[b_1, b_2, \cdots, b_p]$, where $a_i,b_i\in\mathbb{R};\; i\in[1,p]$:

|Vector Addition Definition:|
|:--|
|$A+B=[a_1+b_1, a_2+b_2, \cdots, a_p+b_p]$|

It gets difficult, however, to think of a vector version of multiplication. This will be explored more in depth later.


In addition to vector addition and vector multiplication (again, which will be defined later), operator relationships between vectors (that have multiple field elements) and single field elements must also be defined separately.

Thus, we shall also define **scalar multiplication** (an abbreviation of scalar-vector multiplication) as the multiplying of a field element (scalar) with each element of a vector. For vectors with $p$ different elements per vector,  $A=[a_1, a_2, \cdots, a_p]$ and $r\in\mathbb{F}$:

|Scalar Multiplication Definition:|
|:--|
|$r\cdot A= [ra_1, ra_2, \cdots, ra_p]$|


Now that some simple operations are defined, we shall call a **vector space** $\mathcal{V}$ a set of elements, where each element consists of a collection of field elements from a field $\mathbb{F}$, on which the two operators vector addition and scalar multiplication operate according to the following properties for $A,B,C\in \mathcal{V}\;;\; r,s\in\mathbb{R}$:

|   |Vector Addition|Scalar Multiplication|
|---|:-------------:|:-------------------:|
|**Associativity** | $(A+B)+C=A+(B+C)$ | $(r \cdot s)\cdot A = r \cdot(s \cdot A)$ |
|**Commutativity** | $A+B=B+A$ | $r \cdot A = A \cdot r$ |
|**Identity Element** | $A+0=A$ | $1 \cdot A = A$ |
|**Inverse Element** | $A+(-A)=0$ | $r\cdot \frac{1}{r}\cdot A = A$ |

Then, just like with fields, the above two operations must be related with the final distributive property. For $A,B\in\mathcal{V}$ and $r\in\mathbb{R}$:

|   | Vector Addition, Scalar Multiplication $(+,\cdot)$ |
|:--|:--------------------------------------------------:|
|**Distributivity**| $r \cdot (A+B) = r \cdot A + r \cdot B$|

Similarly to fields, vector spaces are closed under vector addition and scalar multiplication. That means any combination of vector additions and scalar multiplications between vectors in a vector space, will also be in the vector space.

**In summary:** If a set of vectors is closed under an additive vector-vector operation and a multiplicative scalar-vector operation, where each have an associative property, a commutative property, an identity element, and an inverse element, and the operations are related through the distributive property, then it is a vector space.


Examples of vector spaces are:

$$\mathbb{R}^n = \begin{Bmatrix} \begin{pmatrix} \begin{array}{cc} r_1 \\ r_2 \\ \vdots \\ r_n \end{array} \end{pmatrix} : r_1, r_2, \cdots, r_n \in \mathbb{R} \end{Bmatrix}$$

$$\mathbb{R}^2 = \begin{Bmatrix} \begin{pmatrix} \begin{array}{cc} r_1 \\ r_2 \end{array} \end{pmatrix} : r_1, r_2 \in \mathbb{R} \end{Bmatrix}$$

The zero vector in vector field $\mathbb{R}^n$ will be denoted in shorthand as

$$0_n\triangleq \begin{pmatrix} 0 \\ 0 \\ \vdots \\ 0 \end{pmatrix}, 0 \in \mathbb{R}$$

-----
[^1]: In the scope of these notes, I will only cover binary operators, or operators that take two inputs.

[^2]: The expression $(\mathbb{F}\setminus \{0\})$ means "all elements in field $\mathbb{F}$ except for the zero element, $\{0\}$." But why exclude 0?