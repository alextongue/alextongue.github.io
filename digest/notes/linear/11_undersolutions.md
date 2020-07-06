---
title: "11: Underdetermined Systems"
custom_title: Underdetermined Solutions to $Ax=b$
parent: Linear Algebra
grand_parent: Notes
nav_order: 11
---

Consider the equation $Ax=b$, where $A\in\mathbb{R}^{m\times n}, x\in\mathbb{R}^n, b\in\mathbb{R}^m$
- This has a solution if and only if $b\in \mathcal{R}(A)$
- This solution is unique if and only if $\mathcal{N}(A)=\{0\}$
- If there exists some solution $\hat{x}$, then $\hat{x}+x$ is also a solution.

Let there be two solutions to $Ax=b$, $x_1$ and $x_2$.

|LHS||RHS|Explanation|
|--:|:-:|:--|:--|
|$Ax_1$|$=$|$b$||
|$Ax_1-Ax_2$|$=$|$b-b$||
|$A(x_1-x_2)$|$=$|$0$||

This means $(x_1-x_2)\in \mathcal{N}(A) \Rightarrow \mathcal{N}(A)\neq\{0\}$

Furthermore, if $\mathcal{N}(A)=0$, then $A$ has a left inverse.

Therefore, if $A$ has a left inverse, then $Ax=b$ has at most one solution.

If $A$ has a right inverse, then $Ax=b$ has at least one solution.

Let $C$ be a right inverse, so $AC=I_m$. Also let $\hat{x}=Cb$.

|LHS||RHS|Explanation|
|--:|:-:|:--|:--|
|$A\hat{x}$|$=$|$ACb$||
|$A\hat{x}$|$=$|$b$||

In words, applying the left-inverse of A to b yields a solution to the system.


## Actually finding dat solution

For $\mathbb{F}=\mathbb{R}$, we can find a solution to $Ax=b$ easily through QR decomposition.

If $b\in\mathcal{R}(A)$, let A be decomposed into $A=Q[\tilde{R}L]P$, where R is the upper-triangular matrix.

Therefore, $b\in\mathcal{R}(Q)$. So let $\tilde{x}=Q'b$

-----

For $A\in \mathbb{R}^{m\times n}$, the set of solutions of $Ax=b$ (called $X$) is an affine subspace. That means $\{x-x_0 \mid x,x_0\in X\}$ is a linear subspace..

-----

When there are many solutions to $Ax=b$, we are concerned with the least normed solution! In words, we want to find the "smallest" solution $\hat{x}$ that satisfies $\hat{x} = \underset{x:\;Ax=b}{\operatorname{argmin}}({\Vert x\Vert}^2)$ In order to do this, we need the notion of the inverse. Why tho?

For a matrix $A\in \mathbb{F}^{m\times n}$, we say that $A^+\in\mathbb{F}^{n\times m}$ is a **pseudoinverse**, called the Moore-Penrose inverse if it satisfies:
- $AA^+A=A$
- $A^+AA^+=A^+$
- $(AA^+)^\mathbf{H}=AA^+$
- $(A^+A)^\mathbf{H}=A^\mathbf{H}A$

If $A'A$ is invertible, then $A^+=(A'A)^{-1}A'$

If $AA'$ is invertible, then $A^+=A'(AA')^{-1}$

In general, $A^+ = \lim_{\delta\rightarrow0}A'(AA'+\delta^2I)^{-1}$

## to finally solve...
Again, we want to find the value of $x$ such that $\Vert x \Vert^2$ is minimized, or $\hat{x}=\underset{x:\;Ax=b}{\operatorname{argmin}}{\Vert x\Vert^2}$.

Let us claim that $\hat{x}$ is the point that $x-\hat{x} \perp \hat{x}, \forall x:Ax=b$

First, let us observe that for all $x$ that satisfies $Ax=b$ (including $\hat{x}$), the quantity $x-\hat{x}\in \mathcal{N}(A)$

Now we want $\hat{x}\perp\mathcal{N}(A)$, which can imply that $x\in\mathcal{N}(A)$ (why???).

Note that $\mathcal{N}(A)=\mathcal{R}(A')^\perp$.

Therefore, we want $\hat{x}\in\mathcal{R}(A')$, or $\hat{x} = A'z$ for some $z$

Because we want $\hat{x}$ to be a solution to the original system, we still want $A\hat{x}=b$ to hold.

|LHS||RHS|Explanation|
|--:|:-:|:--|:--|
|$A\hat{x}$|$=$|$b$|given|
|$A(A'z)$|$=$|$b$|$\hat{x}=A'z$|
|$z$|$=$|$(AA')^{-1}b$|assume $AA'$ is invertible|
|$A'z$|$=$|$A'(AA')^{-1}b$|left multiply|
|$A'z$|$=$|$A^+b$|pseudoinverse property|
|$\hat{x}$|$=$|$A^+b$|$\hat{x}=A'z$|

We can now verify that for any $x\in\mathcal{N}(A)$, $\hat{x}\perp x$:

$x'\hat{x}=x'A'(AA')^{-1}b \;\Rightarrow\; x'\hat{x}=0(AA')^{-1}b \;\Rightarrow\; x'\hat{x}=0$. This is because we assumed $x\in\mathcal{N}(A)$. Still don't get why.

Let us then verify that this our choice of $\hat{x}$ actually satisfies the equation $\hat{x}=\underset{x:\;Ax=b}{\operatorname{argmin}}{\Vert x\Vert^2}$. For any other solution $y:Ay=b$, $y-\hat{x} \perp \hat{x}$.

|LHS|   |RHS|Explanation|
|--:|:-:|:--|:--|
|$\Vert y\Vert^2$|$=$|$\Vert y\Vert^2$|equality|
| |$=$|$\Vert y-\hat{x}+\hat{x}\Vert^2$|add and subtract|
| |$=$|$2\langle y-\hat{x}, \hat{x}\rangle + \Vert y-\hat{x}\Vert^2 + \Vert\hat{x}\Vert^2$|polarization identity (of norms)|
|$\Vert y\Vert^2$|$=$|$\Vert y-\hat{x}\Vert^2 + \Vert\hat{x}\Vert^2$|$\langle y-\hat{x}, \hat{x}\rangle=0$|
|$\Vert y\Vert^2$|$\geq$|$\Vert \hat{x}\Vert^2$|$\Vert y\Vert^2 \geq 0$|

-----

A pseudoinverse exists for any $A\in\mathbb{R}^{m\times n}$ and is unique.

**Proof:** Suppose that $B$ and $C$ are both pseudoinverses of $A$.

|LHS|   |RHS|Explanation|
|--:|:-:|:--|:--|
|$AB$|$=$|$AB$|equality|
|    |$=$|$(ACA)B$| first property, above|
|    |$=$|$C'A'B'A'$|transpose property|
|    |$=$|$C'(ABA)'$|transpose property|
|    |$=$|$C'A'$|first property, above|
|    |$=$|$AC$|transpose property|

The same equality can be proven backwards, so $CA=BA$. Then,

|LHS|   |RHS|Explanation|
|--:|:-:|:--|:--|
|$B$|$=$|$BAB$|second property, above|
|   |$=$|$B(AC)$|$AB=AC$|
|   |$=$|$(CA)C$|$BA=CA$|
|   |$=$|$C$|second property, above|