---
title: "10: Inverses"
parent: Linear Algebra
grand_parent: Notes
nav_order: 10
layout: default
date: 2020-02-17
---

# Inverses

## Left Inverse

For $A\in\mathbb{F}^{m\times n}, x\in \mathbb{F}^n, Ax\in\mathbb{F}^m$

We say that $A$ has a **left inverse** if $\exists B\in\mathbb{F}^{n\times m} : BA=I_n$.

Let $A$ have a left inverse $B$.

|LHS||RHS|Explanation|
|--:|:-:|:--|:--|
|$Ax$|$=$|$0_m$||
$\;B\cdot Ax$|$=$|$B\cdot0_m$|left-mutiply|
|$x$|$=$|$0_n$|simplify|

$\Longrightarrow$ The only solution to $Ax=0$ is trivial.

$\Longrightarrow\;$ The columns of $A$ are independent.

$\Longrightarrow\; \mathrm{rank}(A) = \mathrm{rank}(A^\mathrm{T}) = n$, or $A$ has full column rank. $A$ must be either square or tall.

$\Longrightarrow\; \forall v\in \mathbb{F}^n, \exists u\in \mathbb{F}^m : u^\mathrm{T}A=v^\mathrm{T}$. Every vector in $\mathbb{F}^n$ can be created through $A$ as a linear combination of the rows in $A$.

$$\;\;\;\;\;\;\;\;[u_1 \rightarrow u_m] \begin{bmatrix} A_{11} & A_{12} & \cdots & A_{1n} \\ \downarrow & \downarrow & \cdots & \downarrow \\ A_{m1} & A_{m2} & \cdots & A_{mn} \\ \end{bmatrix} = [v_1, v_2, \cdots , v_n]$$

$\Longrightarrow\;$ As an extension of the above, a set of $n$ beginning vectors $\{\hat{u}_1, \hat{u}_2, \cdots, \hat{u}_n\}$ could be created such that 

$$ \begin{bmatrix}\hat{u}_{11} & \rightarrow & u_{1m} \\ \hat{u}_{21} & \rightarrow & u_{2m} \\ \vdots & \vdots & \vdots \\ \hat{u}_n & \rightarrow & u_{nm}\end{bmatrix} \begin{bmatrix} A_{11} & A_{12} & \cdots & A_{1n} \\ \downarrow & \downarrow & \cdots & \downarrow \\ A_{m1} & A_{m2} & \cdots & A_{mn} \\ \end{bmatrix} = [e_1, e_2, \cdots, e_n] \Rightarrow \hat{U}A=I_n $$

For complex-valued $A$, let $A^\mathrm{H}A$ not be invertible. That means $\exists x\neq 0_n$, where for $A^\mathrm{H}Ax=0_m$,

|LHS||RHS|Explanation|
|--:|:-:|:--|:--|
|$A^\mathrm{H}Ax$|$=$|$0_m$||
|$x^\mathrm{H}(A^\mathrm{H}Ax)$|$=$|$x^\mathrm{H}(0_m)$|left-multiply|
|$\Vert Ax \Vert^2$|$=$|$0_1$|defintion of L2-norm|
|$Ax$|$=$|$0_m$|property of norm|
||||The columns of $A$ are not indpendent and $A$ does not have a left inverse.

$\therefore A$ has a left inverse if and only if:
- $Ax=0$ does not have a non-trivial solution.
- The columns of A are independent.
- $A^\mathrm{H}A$ is invertible.

## Right Inverse

For $A\in\mathbb{F}^{m\times n}, y\in \mathbb{F}^m, A^\mathrm{T}y\in\mathbb{F}^n$

We say that $A$ has a **right inverse** if $\exists C\in\mathbb{F}^{n\times m} : AC=I_m$.

Let $A$ have a right inverse $C$

|LHS||RHS|Explanation|
|--:|:-:|:--|:--|
|$A^\mathrm{H}y$|$=$|$0_n$||
|$\;C^\mathrm{H}A^\mathrm{H}y$|$=$|$C^\mathrm{H}0_n$|left-multiply|
|$(AC)^\mathrm{H}y$|$=$|$0_m$|definition of transpose|
|$y$|$=$|$0_m$|definition of right-inverse|

$\Longrightarrow$ The only solution to $A^\mathrm{H}y=0$ is trivial.

$\Longrightarrow$ The rows of $A$ are linearly independent.

$\Longrightarrow$ $\mathrm{rank}(A^\mathrm{H}) = \mathrm{rank}(A)=m$, or $A$ has full row rank. $A$ must be either fat or square.

Assume that $AA^\mathrm{H}$ is not invertible. That means $\exists y \neq 0_m$, where for $AA^\mathrm{H}y=0_m$,

|LHS||RHS|Explanation|
|--:|:-:|:--|:--|
|$AA^\mathrm{H}y$|$=$|$0_m$||
|$y^\mathrm{H}AA^\mathrm{H}y$|$=$|$y^\mathrm{H}\cdot 0_m$|left-multiply|
|$\Vert A^\mathrm{H}y \Vert^2$|$=$|$0_1$|definition of L2 norm|
|$A^\mathrm{H}y$|$=$|$0_n$|property of norm|
||||the columns of $A^\mathrm{H}$ are not linearly independent and $A^\mathrm{H}$ does not have a left inverse.|

$\therefore A$ has a right inverse if and only if:
- $A^\mathrm{H}x=0$ does not have a non-trivial solution.
- The rows of A are independent.
- $AA^\mathrm{H}$ is invertible.