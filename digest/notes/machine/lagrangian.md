---
title: Lagrangian Multiplier
nav_order: 5
parent: Machine Learning, Data Science
grand_parent: Notes
---

Let us find the values of $x,y,z$ that yield extrema in the function $f(x,y,z)$ given a constraint that $g(x,y,z)=k$.


First, let us set up the following system of equations, and then figure out how this optimizes the function $f$.

$$
(1)\;\;\;\triangledown f(x,y,z) = \lambda \triangledown g(x,y,z)
$$

$$(2)\;\;\;g(x,y,z)=k$$

Recall that the gradient of a function of some number of variables contains that same number of components. In the above case, equation $(1)$ actually has three components that must be equal, resulting in four equations:

$$(\mathrm{1a})\;\;\;f_x=\lambda g_x$$

$$(\mathrm{1b})\;\;\;f_y=\lambda g_y$$

$$(\mathrm{1c})\;\;\;f_z=\lambda g_z$$

$$(2)\;\;\;g(x,y,z)=k$$

Equations $(1)$ states that functions $f$ and $g$ must be tangent at their solution; because their components must be equal, their gradient will be pointing in the same direction. Equation $(2)$, then, simply states that the constraint of $g$ must be met.


## Lagrange Multipliers for SVM

Recall that for a support vector machine (SVM), we have two extrema to find:
- Find the maximum sum of margins over all points
- Find the value of $\mathrm{w}$ with the minimum norm

Because the regularizer counteracts the margin function, we want to find a maximum and a minimum at the same time. This is the equivalent to minimizing the regularizer the negative of the margin

$$
\min_{\mathbf{w},b}(\mathrm{reg}(\mathbf{w}) - \mathrm{marg}(\mathbf{w},b))
$$

or maximizing the negative of the regularizer and the margin

$$
\max_{\mathbf{w},b}(-\mathrm{reg}(\mathbf{w}) + \mathrm{marg}(\mathbf{w},b))
$$

We have chosen the first: to find the minimum. Let us now recall what we came up with for the regularized SVM loss function:

$$
L(\mathbf{w},b) = \frac{1}{2}\| \mathbf{w}\|^2 - \sum_{n=1}^N\big( t_n(\mathbf{w}^\mathrm{T}\mathbf{x}_n + b) - 1 \big)
$$

Let us add a Lagrange multiplier to the loss function for each training point, $a_1, a_2, \cdots, a_N$:

$$
L(\mathbf{w},b) = \frac{1}{2}\| \mathbf{w}\|^2 - \sum_{n=1}^N a_n \big( t_n(\mathbf{w}^\mathrm{T}\mathbf{x}_n + b) - 1 \big)
$$

and expand the sums

$$
L(\mathbf{w},b) = \frac{1}{2}\| \mathbf{w}\|^2 - \sum_{n=1}^N \big(a_n t_n \mathbf{w}^\mathrm{T}\mathbf{x}_n + a_n t_n b - a_n \big)
$$

$$
L(\mathbf{w},b) = \frac{1}{2}\| \mathbf{w}\|^2 - \sum_{n=1}^N a_n t_n \mathbf{w}^\mathrm{T}\mathbf{x}_n - b\sum_{n=1}^N{a_n t_n} + \sum_{n=1}^N a_n 
$$

To find the optimal values of $\mathbf{w}$ and $b$ that yield the extrema of the loss, we set the derivatives with respect to each variable to zero, starting with $\mathbf{w}$:

$$0 = \frac{dL}{d\mathbf{w}}$$

$$0 = \mathbf{w} - \sum_{n=1}^N{a_n t_n \mathbf{x}_n} - 0 + 0$$

$$\mathbf{w}_\mathrm{opt} = \sum_{n=1}^N{a_n t_n \mathbf{x}_n} \triangleq \tilde{\mathbf{w}} $$

and then for $b$:

$$0 = \frac{dL}{db}$$

$$0=0 - 0 - \sum_{n=1}^N{a_n t_n} + 0$$

$$\sum_{n=1}^N{a_n t_n}=0$$

Now, we substitute these definitions back into the loss function for the optimized $L$, denoted $\tilde{L}$:

|LHS||RHS|Explanation|
|--:|:-:|:--|:--|
| $$\tilde{L}$$ | $$=$$ | $$\frac{1}{2}\tilde{\Vert\mathbf{w}}\Vert^2 - \sum_{n=1}^N a_n t_n \tilde{\mathbf{w}}^\mathrm{T}\mathbf{x}_n - b\sum_{n=1}^N{a_n t_n} + \sum_{n=1}^N a_n$$ | loss function |
||$$=$$| $$\frac{1}{2} \tilde{\mathbf{w}}^\mathrm{T} \tilde{\mathbf{w}} - \sum_{n=1}^N a_n t_n \tilde{\mathbf{w}}^\mathrm{T}\mathbf{x}_n - b\sum_{n=1}^N{a_n t_n} + \sum_{n=1}^N a_n$$ | expand $$\|\mathbf{w}\|^2$$ |
||$$=$$| $$\frac{1}{2} \bigg(\sum_{m=1}^N{a_m t_m \mathbf{x}_m}\bigg) \bigg(\sum_{n=1}^N{a_n t_n \mathbf{x}_n}\bigg) - \sum_{n=1}^N a_n t_n \bigg(\sum_{m=1}^N{a_m t_m \mathbf{x}_m}\bigg) \mathbf{x}_n - b\sum_{n=1}^N{a_n t_n} + \sum_{n=1}^N a_n$$ | $$\tilde{\mathbf{w}} = \sum_{n=1}^N{a_n t_n \mathbf{x}_n}$$|
||$$=$$| $$\frac{1}{2} \sum_{n=1}^N\sum_{m=1}^N{a_n a_m t_n t_m \mathbf{x}_n \mathbf{x}_m} - \sum_{n=1}^N \sum_{m=1}^N {a_n a_m t_n t_m \mathbf{x}_n \mathbf{x}_m} - b\sum_{n=1}^N{a_n t_n} + \sum_{n=1}^N a_n$$ | rearrange sums|
||$$=$$| $$-\frac{1}{2} \sum_{n=1}^N\sum_{m=1}^N{a_n a_m t_n t_m \mathbf{x}_n \mathbf{x}_m} - b\sum_{n=1}^N{a_n t_n} + \sum_{n=1}^N a_n$$ | subtract common terms |
||$$=$$| $$-\frac{1}{2} \sum_{n=1}^N\sum_{m=1}^N{a_n a_m t_n t_m \mathbf{x}_n \mathbf{x}_m} - b(0) + \sum_{n=1}^N a_n$$ | $$\sum_{n=1}^N{a_n t_n}=0$$ |
||$$=$$| $$\sum_{n=1}^N a_n -\frac{1}{2} \sum_{n=1}^N\sum_{m=1}^N{a_n a_m t_n t_m \mathbf{x}_n \mathbf{x}_m}$$ | rearrange terms |

Now we parameterize with respect to the vector $\mathbf{a}$:

$$
\tilde{L}(\mathbf{a}) = \sum_{n=1}^N a_n -\frac{1}{2} \sum_{n=1}^N\sum_{m=1}^N{a_n a_m t_n t_m \mathbf{x}_n \mathbf{x}_m}
$$

and maximize it while remembering the constraint

$$\sum_{n=1}^N{a_n t_n}=0$$