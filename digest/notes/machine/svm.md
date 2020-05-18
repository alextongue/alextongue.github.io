---
title: Support Vector Machine
nav_order: 4
parent: Machine Learning, Data Science
grand_parent: Notes
layout: notes
---

# Support Vector Machine

A support vector machine (SVM) is one that classifies a dataset based on:

- misclassifications
- a margin for misclassification


Because there is a margin that allows for a certain extent of misclassifications to occur, an SVM is theoretically able to find a linear decision rule to classify nonlinearly separable data.

## Neural Network Beginning

Let there be an input matrix $\mathbf{X}$ made up of $N$ input vectors $\mathbf{x} \in \mathbb{R}^D$, where

$$
\mathbf{X} = \begin{bmatrix} \mathbf{x}_1 & \mathbf{x}_2 & \cdots & \mathbf{x}_N \\ \downarrow & \downarrow & \cdots & \downarrow \end{bmatrix} \in \mathbb{R}^{D\times N}
$$

For each input vector $\mathbf{x}_i$, there will also be an associated scalar training label $t_i \in \mathbb{R}$ that denotes the actual label/class of the input vector.

> For the sake of this example, let's say that we're looking at two labels, and let's define numerically by saying that it can take one of two values: $t\in \begin{Bmatrix}-1, 1 \end{Bmatrix}$

All of the labels can be aggregately expressed as a vector

$$
\mathbf{t} = \begin{bmatrix}t_1 \\ t_2 \\ \vdots \\ t_N\end{bmatrix} \in \mathbb{R}^N
$$

Let a transformation matrix $\mathbf{w} \in \mathbb{R}^{D}$ and bias vector affinely estimate an output given an input, denoted as $y(\mathbf{x}_i) \in \mathbb{R}$:

$$
y(\mathbf{x}_i) = \mathbf{w}^\mathrm{T}\mathbf{x}_i + b
$$

And let  a loss function would be usually calculated by comparing the estimate/output to the label $t_i$.

$$
L(\mathbf{x}_i, y(\mathbf{x}_i), t_i) = y(\mathbf{x}_i) \cdot t_i
$$

### Interpreting the Loss, Spelled Out

Recall that we had defined $t$ to be a binary variable that takes arbitrary values $-1$ and $1$. This definition conveninently allows for an intuitive understanding of our estimator $y(\cdot)$ as a decision boundary:

For some input datapoint $\mathbf{x}_i$:
 - If $y(\mathbf{x}_i) > 0$, our machine states that the point is closer to the **positive** class $t=+1$
 - If $y(\mathbf{x}_i) < 0$, our machine states that the point is closer to the **negative** class $t=-1$

From this, we can also intuitively understand how this machine returns losses depending on whether or not is classifying correctly. Here are correct classifications, case-wise:

- If $y(\mathbf{x}_i) > 0$ and $t=+1$, that means our machine had correctly classified into the **positive** class.
- If $y(\mathbf{x}_i) < 0$ and $t=-1$, that means our machine had correctly classified into the **negative** class.

In both of the above cases, numbers of the same sign are being multiplied, which yields $L(\mathbf{x}_i, y(\mathbf{x}_i), t_i) > 0$.

And here are incorrect classifications, case-wise:

- If $y(\mathbf{x}_i) > 0$ and $t=-1$, that means our machine had incorrectly classified into the **positive** class.
- If $y(\mathbf{x}_i) < 0$ and $t=+1$, that means our machine had incorrectly classified into the **negative** class

In the above cases, numbers of opposite sign are being multiplied, which yields $L(\mathbf{x}_i, y(\mathbf{x}_i), t_i) < 0$.

What is worth noting is that because we had defined the class labels to be either $t=1$ or $t=-1$. That means whether the classification is correct or incorrect only changes the sign of the loss, and the magnitudes of the estimators are preserved. This allows for us to express two estimate qualities using one number. For example:

- If $y(\mathbf{x}_i)t_i$ is positive and small, we can interpret that our classifier was "correct by a small margin"
- If $y(\mathbf{x}_i)t_i$ is negative and large, we can interpret that our classifier was "incorrect by a  large margin" 

## Bridging the Gap from NN to SVM

To summarize the neural network setup above, an input vector $\mathbf{x}_i$ is

- multiplied by a bunch of weights $W$ and
- outputs $y(\mathbf{x}_i)$,
- from which a loss $L(\mathbf{x}_i, y(\mathbf{x}_i), t_i)$ is calculated.


Now, this by itself *almost* resembles a single linear layer of a feed-forward network. When passing all datapoints through this network, the sum of losses would be calculated either in matrix form

$$
L(\mathbf{X}, y(\mathbf{X}), \mathbf{t}) = (\mathbf{w}^\mathrm{T} \mathbf{X} + \mathbf{1}b) \cdot \mathbf{t}
$$

or as an equivalent sum of individual vectors:

$$
L(\mathbf{X}, y(\mathbf{X}), \mathbf{t}) = \sum_{i=1}^{N}{((\mathbf{w}^\mathrm{T} \mathbf{x}_i + b) \cdot t_i)}
$$

**So what makes an SVM different?**

Remember, SVM stands for Support Vector Machine. A for an SVM, we are also concerned about the loss at the datapoint closest to the boundary, and we can neglect all other losses.

We still care about the misclassification, and this is actually where our SVM diverges into two types:
- Soft Margin SVM?
- Kernel SVM?

For this flavor of SVM, we only care about the points that are correctly classified and closest to our decision boundary. If you recall the section above where our loss is explicitly interpreted, that means we are looking for the **smallest positive** value[^1] of $L$

$$
\min_n(L) = \min_n \bigg( \frac{(\mathbf{w}^\mathrm{T}\mathbf{x}_n+b) t_n}{\| \mathbf{w} \|} \bigg)
$$

For sake of simplicity, we can move the norm of $\mathbf{w}$ outside of the minimum function.

$$
\min_n(L) = \frac{1}{\| \mathbf{w}\| } \min_n \big( (\mathbf{w}^\mathrm{T}\mathbf{x}_n+b) t_n \big)
$$


Now, we want to find the optimal values of weights and bias that maximize that quantity:

$$
\mathbf{w}_\mathrm{opt}, b_\mathrm{opt} = \argmax_{\mathbf{w},b} \bigg( \frac{1}{\| \mathbf{w}\| } \min_n \big( (\mathbf{w}^\mathrm{T}\mathbf{x}_n+b) t_n \big)\bigg)
$$



## Footnotes
[^1]: Note that we are looking for the $\min(\cdot)$, not the $\argmin(\cdot)$; the former returns the actual minimized argument, while the latter returns the argument instead. In this case, we have no use of the specific index $n_\mathrm{min}$ returned.