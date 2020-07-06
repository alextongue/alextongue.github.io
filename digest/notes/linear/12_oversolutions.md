---
title: "12: Overdetermined Systems"
custom_title: Overdetermined Solutions to $Ax=b$
parent: Linear Algebra
grand_parent: Notes
nav_order: 12
---

Sometimes there is no solution of $x$ to $Ax=b$. The matrix A is usually tall.

First, we will change $b$ to some $\hat{b}$ that is as close as possible to the original $b$.

Like the least-normed solution, we can show that once we obtain some $\hat{b}\in\mathcal{R}(A)$, or $Ax=\hat{b}$, we can then find the optimal solution $\hat{x}$ such that $A\hat{x}=\hat{b}$.

First, let us QR decompose $A$ into $A=QR$.

Then we will write $b-QQ'b \perp \mathcal{R}(A)$.

Note that $b-QQ'b = b - \langle b,q_1\rangle q_1 - \langle b,q_2\rangle q_2 - \cdots - \langle b,q_k\rangle q_k$. The above orthogonality statement is true because we are subtracting all of the influence of $A$ from $b$. So we are left with some version of $b$ that is orthogonal to all basis vectors of $A$. We will call this $\hat{b}$.

Note that where $QQ'b=\hat{b}$

$(I-QQ')b \perp \mathcal{R}(A)$, where



Now we will use QR decomposition to find $\hat{x}$ for $A\hat{x}=\hat{b}$.

$A=Q[\tilde{R}T]P$, where $\tilde{R}$ is upper triangular, $P$ is a permutation matrix, and $T$ is something else. Then, $\hat{x}=P^{-1}\begin{bmatrix}\tilde{R}^{-1} \\ 0\end{bmatrix}$.

## Another way to solve Ax=b

Let us notice that $b-A\hat{x} \perp \mathcal{R}(A)$.

Therefore, $A^\mathrm{T}A=A^\mathrm{T}A\hat{x}$.

If $A^\mathrm{T}A$ is invertible, then $\hat{x}=(A^\mathrm{T}A)^{-1}A^\mathrm{T}b=A^+b$.
