---
title: Regression Tree Classifier 
date: 2020-04-09
nav_order: 3
parent: Machine Learning, Data Science
grand_parent: Notes
layout: default
---

# Regression Tree Classifier

Given a set of n-dimensional datapoints $\mathcal{X} = \begin{Bmatrix} \mathbf{x}_1, \mathbf{x}_2, \cdots, \mathbf{x}_N\end{Bmatrix} \in \mathbb{R}^{n}$, we can iteratively divide $\mathcal{X}$ into discrete groups using a **regression tree**.

Each branch of the tree represents a division based on one or more dimensions. For decision trees, this division is binary and disjoint. this means all of the points arriving at a given branch are classified into one of its branches. 

## Let's start with an example.

For example, let us consider a dataset of six points in two dimensions. Furthermore, for the sake of simplicity, we will only consider divisions across one dimension at a time.

$$
\mathcal{D}=\begin{Bmatrix}
\begin{bmatrix}1\\10\end{bmatrix},
\begin{bmatrix}1\\88\end{bmatrix},
\begin{bmatrix}2\\23\end{bmatrix},
\begin{bmatrix}8\\109\end{bmatrix},
\begin{bmatrix}4\\76\end{bmatrix},
\begin{bmatrix}9\\74\end{bmatrix}
\end{Bmatrix}
$$

The dimensions will be notated as
$$\begin{bmatrix} \mathbf{x}_{(1)} \\ \mathbf{x}_{(2)}\end{bmatrix} \in \mathbb{R}^{2}$$ 

## **Step 1:** Set a Decision Boundary

To begin, let's construct the first tree branch by drawing a boundary on the first dimension. How about we arbitrarily choose the boundary $t_1 = 5$ and apply it to $\mathbf{x}_{(1)}$? That seems like a nice median value of the first dimension.

## **Step 2:** Split Data Based on the Decision

So let's take our incoming set (which is, in this case, the original dataset) and call it $\mathcal{S_{t_1}}$ The boundary $t_1$ will split $\mathcal{S_{t_1}}$ into the following two subsets:

$$
\mathcal{S}_{t_1,1}=\begin{Bmatrix}\mathbf{x}_i | \mathbf{x}_{i(1)}\leq t_1,\; i\in[1,N]\end{Bmatrix}
$$

$$
\mathcal{S}_{t_1,2}=\begin{Bmatrix}\mathbf{x}_i | \mathbf{x}_{i(1)} > t_1,\; i\in[1,N]\end{Bmatrix}
$$

By plugging in our set $\mathcal{D}$ and boundary $t_1=5$, we have

$$
\mathcal{S}_{t_1,1}=\begin{Bmatrix}\mathbf{x}_i | \mathbf{x}_{i(1)}\leq 5,\; i\in[1,6]\end{Bmatrix}
$$

$$
\mathcal{S}_{t_1,2}=\begin{Bmatrix}\mathbf{x}_i | \mathbf{x}_{i(1)} > 5,\; i\in[1,6]\end{Bmatrix}
$$

which is evaluated to the following:

$$
\mathcal{S}_{t_1,1}=\begin{Bmatrix}
\begin{bmatrix}1\\10\end{bmatrix},
\begin{bmatrix}1\\88\end{bmatrix},
\begin{bmatrix}2\\23\end{bmatrix},
\begin{bmatrix}4\\76\end{bmatrix}
\end{Bmatrix}\;\;\;
$$

$$
\mathcal{S}_{t_1,2}=\begin{Bmatrix}
\begin{bmatrix}8\\109\end{bmatrix},
\begin{bmatrix}9\\74\end{bmatrix}
\end{Bmatrix}
$$

But how do we know that the arbitrary boundary value that we chose is the best value to divide our set? Let's create some function that returns a score[^1] of how badly our division splits up our data! This is called a loss function.

## **Step 3:** Create a Loss Function For the Branched Sets

A **loss function** is some metric that describes the effectiveness of our boundary given our data.

We want to know how good each branch does in classifying the data that was thrown into it. We will call this a **branch loss**. One possible branch loss for our classification problem could be the sum of distances between each binned value and the mean of the values in that bin, across the dimension(s) that we have drawn our boundary over.

Because we want to penalize losses for all distances -- positive or negative -- let's take the absolute value of these differences $(\vert\cdot\vert)$ before adding them up. That will make things less confusing. To avoid this source of confusion in the future, we will use norms. Think of a norm as a distance with some nice properties that make it easier to intuitively interpret as distance. In this case, taking the sum of absolute values is called the **L1 norm**, $\Vert \cdot \Vert_1$.

So for our first set $\mathcal{S}\_{t_1,1}$, let's take the average of its member values' across the first dimension $\mathbf{x}_{(1)}$ 

$$
\overline{\mathcal{S}_{t_1,1}} = \frac{1+1+2+4}{4}=2
$$

then find the absolute-value differences between each value and that mean and take its L1 norm

$$
\mathrm{Loss}(\mathcal{S}_{t_1,1}) = \Vert \mathbf{x_{(1)}} - \overline{\mathcal{S}_{t_1,1}}\Vert_{1}\; \mathrm{across}\; {\mathbf{x}\in \mathcal{S}_{t_1,1}}
$$

$$
\mathrm{Loss}(\mathcal{S}_{t_1,1}) = \sum_{\mathbf{x}\in \mathcal{S}_{t_1,1}}{\vert\mathbf{x_{(1)}} - \overline{\mathcal{S}_{t_1,1}}\vert}
$$

$$
= \vert 1-2\vert + \vert 1-2\vert + \vert 2+2\vert + \vert 4-2\vert
$$

$$ = 1+1+0+2 $$

$$ =4 $$

Let's do the same thing for the $\mathcal{S}_{t_1,2}$:

$$
\overline{\mathcal{S}_{t_1,2}} = \frac{8+9}{2} = 8.5
$$

$$
\mathrm{Loss}(\mathcal{S}_{t_1,2}) = \sum_{\mathbf{x}\in \mathcal{S}_{t_1,2}}{\vert\mathbf{x_{(1)}} - \overline{\mathcal{S}_{t_1,2}}\vert}
$$

$$ = \vert 8-8.5\vert + \vert 9-8.5\vert $$

$$ = 0.5 + 0.5 $$

$$ =1 $$

## **Step 4:** Create a Total Loss Function that Combines Branch Losses

So far, we have branch losses of 4 and 1. We know these values will be well-conditioned because they will always be positive, and they accumulate (as our idea of a loss should). But how do we interpret two numbers when we're trying to evaluate a single boundary? How can we turn these two numbers into one? Let's add them up!

$$
\mathrm{Loss_{T}}(\mathcal{S_{t_1}}) = \mathrm{Loss}(\mathcal{S}_{t_1,1}) + \mathrm{Loss}(\mathcal{S}_{t_1,2}) = 4 + 1 = 5
$$

Let's call this aggregate loss the **total loss** and denote it with that subscripted little uppercase T. In this example, the total loss was just the sum of branch losses, but we can use a more complex function in the future.

So we know that this total loss is ultimately derived from the sum of differences between each group's value and its mean value. And we want to find the boundary that gives us the lowest total loss. But is 5 the lowest number? Not sure. Let's shift the boundary $t_1$ around so that different data points move between branches $\mathcal{S}_{t_1,1}$ and $\mathcal{S}_{t_1,2}$. All of these tweaks (including the above one) is summarized in the following table:

|$$t_1$$ | $$\mathcal{S}_{t_1,1}$$|$$\mathcal{S}_{t_1,2}$$ | $$\mathrm{Loss}(\mathcal{S}_{t_1,1})$$ | $$\mathrm{Loss}(\mathcal{S}_{t_1,1})$$ | $$\mathrm{Loss_{T}}(\mathcal{S_{t_1}})$$|
|:-:|:-:|:-:|:-:|:-:|:-:|
| $$-1000$$ | $$\begin{Bmatrix}\\\end{Bmatrix}$$ | $$\begin{Bmatrix} \begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix} \end{Bmatrix}$$ |$$0$$|$$4.1667$$|$$4.1667$$|
| $$0$$ | $$\begin{Bmatrix}\\\end{Bmatrix}$$ | $$\begin{Bmatrix} \begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix} \end{Bmatrix}$$ |$$0$$|$$4.1667$$|$$4.1667$$|
| $$1.5$$ | $$\begin{Bmatrix}\begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}\end{Bmatrix}$$ | $$\begin{Bmatrix}\begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix}\end{Bmatrix}$$ |$$1$$|$$5.75$$|$$6.75$$|
| $$3$$ | $$\begin{Bmatrix}\begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}\end{Bmatrix}$$ | $$\begin{Bmatrix} \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix}\end{Bmatrix}$$ |$$1.3333$$|$$7$$|$$8.3333$$|
| $$5$$ | $$\begin{Bmatrix}\begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}\end{Bmatrix}$$ | $$\begin{Bmatrix} \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix}\end{Bmatrix}$$ |$$4$$|$$1$$|$$5$$|
| $$5.01$$ | $$\begin{Bmatrix}\begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}\end{Bmatrix}$$ | $$\begin{Bmatrix} \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix}\end{Bmatrix}$$ |$$4$$|$$1$$|$$5$$|
| $$8.5$$ | $$\begin{Bmatrix}\begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}8\\109\end{bmatrix}\end{Bmatrix}$$ | $$\begin{Bmatrix}\begin{bmatrix}9\\74\end{bmatrix}\end{Bmatrix}$$ |$$3.2$$|$$9$$|$$12.2$$|
| $$10$$ | $$\begin{Bmatrix} \begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix} \end{Bmatrix}$$ | $$\begin{Bmatrix}\\\end{Bmatrix}$$ |$$4.1667$$|$$0$$|$$4.1667$$|
| $$1000$$ | $$\begin{Bmatrix} \begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix} \end{Bmatrix}$$ | $$\begin{Bmatrix}\\\end{Bmatrix}$$ |$$4.1667$$|$$0$$|$$4.1667$$|

From the table, we can tell that the lowest possible loss is 4.1667, which is achieved for boundaries $t_1 <1$ or $t_1\geq 9$. Is that great? Not really.

The problem is this: We found the boundary that gives us the lowest total loss, but classification didn't really take place -- we just threw every value into one bin and left the other empty. It seems like our loss function is still a little ambiguous -- it's not well-behaved enough.

> **Question:** How can we tweak our loss function to make the best boundary a stand out more clearly?
> 
> **Answer:** Let's introduce a regularization parameter!

## **Step 5:** Apply Loss Regularization

Think of **regularization** as adding constraints that measure different parts of our loss function and add that measure to our loss function. It's most useful if it "works against" or limits the unhindered growth of our original loss. Some general examples of regularization are:

- We want to fit data with polynomial coefficients $\mathbf{p} = \begin{Bmatrix} p_0, p_1, p_2, \cdots, p_n\end{Bmatrix}$,[^2] but we don't want to overfit data with a function that is too complex (or "wiggly"). So we will introduce the L2 norm of the polynomial, $\Vert\mathbf{p}\Vert_2$. If this norm is new to you, you just need to know that the L2 norm returns a larger value for "smoother" vectors[^3] (e.g. a vector whose coefficient values are spread out more evenly)

$$\Vert \mathbf{p} \Vert_2 = \sqrt{\sum_{i=0}^{N}{p_i^2}}$$

- We want to split our data into groups, but we want the splits to result in groups that are close in size. So we will introduce a term $R$ that subtracts from the loss if the difference in size between sets is small:

$$R(\mathcal{S}_{t_1,1}, \mathcal{S}_{t_1,2}) = \vert \mathrm{size}(\mathcal{S}_{t_1,1}) - \mathrm{size}(\mathcal{S}_{t_1,2})\vert$$

That second example describes our case pretty well. Let's use that. As a reminder, our original loss function takes the first dimension and measures each member's distance from the set mean:

$$\mathrm{further\;from\;mean} \Rightarrow \mathrm{bad} \Rightarrow \mathrm{more\;loss}\Rightarrow \mathrm{add\;to\;Loss()}$$

Before we throw in our regularization parameter, we need to think about whether or not we should add or subtract this parameter. Let's look at how we should interpret $R$.

$$\mathrm{bigger\;size\;difference} \Rightarrow \mathrm{bad} \Rightarrow \mathrm{more\;loss}\Rightarrow \mathrm{add\;to\;Loss()}$$

It looks like we can just add it to our loss function! But if we look at the range of this regularization parameter, it looks pretty large. We don't want this parameter to dominate the total loss function and overshadow our main distance-from-mean function. So let's scale $D$ down by multiplying it by $\lambda = 0.25$. This finally results in the following total loss:

$$
\mathrm{Loss_{T}}(\mathcal{S_{t_1}}) = \mathrm{Loss}(\mathcal{S}_{t_1,1}) + \mathrm{Loss}(\mathcal{S}_{t_1,2}) + \lambda R(\mathcal{S}_{t_1,1}, \mathcal{S}_{t_1,2})
$$

$$
\mathrm{Loss_{T}}(\mathcal{S_{t_1}}) = \mathrm{Loss}(\mathcal{S}_{t_1,1}) + \mathrm{Loss}(\mathcal{S}_{t_1,2}) + 0.25 R(\mathcal{S}_{t_1,1}, \mathcal{S}_{t_1,2})
$$


Now let's reconstruct that table of boundaries from above, now with the regularization parameter.

|$$t_1$$ | $$\mathcal{S}_{t_1,1}$$|$$\mathcal{S}_{t_1,2}$$ | $$\mathrm{Loss}(\mathcal{S}_{t_1,1})$$ | $$\mathrm{Loss}(\mathcal{S}_{t_1,1})$$ | $$\lambda R(\mathcal{S}_{t_1,1}, \mathcal{S}_{t_1,2})$$ | $$\mathrm{Loss_{T}}(\mathcal{S_{t_1}})$$ with $$\lambda D$$|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| $$-1000$$ | $$\begin{Bmatrix}\\\end{Bmatrix}$$ | $$\begin{Bmatrix} \begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix} \end{Bmatrix}$$ |$$0$$|$$4.1667$$|$$(9)(0.25)=2.25$$|$$6.4167$$|
| $$0$$ | $$\begin{Bmatrix}\\\end{Bmatrix}$$ | $$\begin{Bmatrix} \begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix} \end{Bmatrix}$$ |$$0$$|$$4.1667$$|$$(9)(0.25)=2.25$$|$$6.4167$$|
| $$1.5$$ | $$\begin{Bmatrix}\begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}\end{Bmatrix}$$ | $$\begin{Bmatrix}\begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix}\end{Bmatrix}$$ |$$1$$|$$5.75$$|$$(2)(0.25)=0.5$$|$$7.25$$|
| $$3$$ | $$\begin{Bmatrix}\begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}\end{Bmatrix}$$ | $$\begin{Bmatrix} \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix}\end{Bmatrix}$$ |$$1.3333$$|$$7$$|$$(0)(0.25)=0$$|$$8.3333$$|
| $$5$$ | $$\begin{Bmatrix}\begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}\end{Bmatrix}$$ | $$\begin{Bmatrix} \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix}\end{Bmatrix}$$ |$$4$$|$$1$$|$$(2)(0.25)=0.5$$|$$5.5$$|
| $$5.01$$ | $$\begin{Bmatrix}\begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}\end{Bmatrix}$$ | $$\begin{Bmatrix} \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix}\end{Bmatrix}$$ |$$4$$|$$1$$|$$(2)(0.25)=0.5$$|$$5.5$$|
| $$8.5$$ | $$\begin{Bmatrix}\begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}8\\109\end{bmatrix}\end{Bmatrix}$$ | $$\begin{Bmatrix}\begin{bmatrix}9\\74\end{bmatrix}\end{Bmatrix}$$ |$$3.2$$|$$9$$|$$(4)(0.25)=1$$|$$13.2$$|
| $$10$$ | $$\begin{Bmatrix} \begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix} \end{Bmatrix}$$ | $$\begin{Bmatrix}\\\end{Bmatrix}$$ |$$4.1667$$|$$0$$|$$(9)(0.25)=2.25$$|$$6.4167$$|
| $$1000$$ | $$\begin{Bmatrix} \begin{bmatrix}1\\10\end{bmatrix}, \begin{bmatrix}1\\88\end{bmatrix}, \begin{bmatrix}2\\23\end{bmatrix}, \begin{bmatrix}8\\109\end{bmatrix}, \begin{bmatrix}4\\76\end{bmatrix}, \begin{bmatrix}9\\74\end{bmatrix} \end{Bmatrix}$$ | $$\begin{Bmatrix}\\\end{Bmatrix}$$ |$$4.1667$$|$$0$$|$$(9)(0.25)=2.25$$|$$6.4167$$|

Now it looks like our lowest total loss is achieved with our original value $t=5$. And it seems to split our groups in a meaningful way! But here are two more questions:

> **Question:** We can see that choosing of $t_1<1$ is in effect, identical as choosing $t_1\geq 9$: both ranges classify all of the values into one bin and leave the other bin empty. There doesn't seem to be any strict symmetry in boundaries otherwise (e.g. $t_1=1.5$ and $t_1=8.5$ do not result in the same sets). Is this an issue?
> 
> **Answer:** This isn't really an issue. For any dataset, it seems like this sense of symmetry only occurs at the edge regions where one bin holds all the data and the other is empty. Provided that we tweak $\lambda$ enough for our boundary to move away from these regions, this is an ambiguity that we can keep.

> **Question:** Similarly to the above question: Because we're working with discrete data points, It also seems like there are entire ranges of boundaries that result in the same division of branches. For example, $t_1=\begin{Bmatrix} (-\infty, 1), [9, \infty)\end{Bmatrix}$ seem to split our training set into the same branches. Same thing happens for range as well as $t_1=\begin{Bmatrix} [1, 2)\end{Bmatrix}$, $t_1=\begin{Bmatrix} [2, 4)\end{Bmatrix}$, and so on. Because our loss function only depends on splitting up discrete training points, how do we know that where between points to draw the boundaries?
> 
> **Answer:** We can implement other regularization functions that depend on relative distances between nearby points. For example, we can take a boundary and weight its total loss depending on its distances between nearby points. This type of regularization that aims to converge on the best linear separator in a range of "already good values" has actually become a foundational part of building a support vector machine (SVM), and is known as margin optimization.
> 
> In effect, this parameter will turn an otherwise flat loss region (see figure) into a continuous surface, with the lowest value being at contours of equal distance between training points (k-nearest neighbor).

## Build more Branches!

To recap, here's what we've done to fleshed out our first branch (I reworded the steps to hopefully make it easy to see how you can manually implement an algorithm):

- **Step 1:** Choose a decision boundary:

$$t_1$$

- **Step 2:** Split data into branches based on the decision:

$$\mathcal{S}_{t_1} = \begin{Bmatrix} \mathcal{S}_{t_1,1}, \mathcal{S}_{t_1,2}\end{Bmatrix}$$
  
- **Step 3:** Calculate a branch loss for each set.

$$\mathrm{Loss}(\mathcal{S}_{t_1,1}),\;\mathrm{Loss}(\mathcal{S}_{t_1,1})$$

- **Steps 4, 5:** Calculate total loss that combines branch losses with regularization.

$$\mathrm{Loss}_\mathrm{T}(\mathcal{S}_{t_1}) = \mathrm{Loss}(\mathcal{S}_{t_1,1}) + \mathrm{Loss}(\mathcal{S}_{t_1,2}) + \lambda R(\mathcal{S}_{t_1,1}, \mathcal{S}_{t_1,2})$$

- **Step 6:** Repeat Steps 1-5; change values of the decision boundary until the minimum total loss is achieved.

If you follow this iterative process, then you should be able to split your incoming data into some nice subsets! At this point, you continue to build yuor tree by following the same steps for each branch. The branches will split into more branches, and you'll find that you made a structure that resembles a tree.

I continued our example for a couple more stages, and I ended up with the following tree:

(figure)

Another neat way to express this split is to assign each dimension (feature) to an axis on a graph. However, this graphical method completely depicts the tree only if we have 3 or less dimensions, because it gets hard for us to visualize more than three dimensions. We'd have to look to some methods to reduce dimensionality, which will be explained later.

## Final Thoughts

Question: How does this work with regression?

Question: When do I know that it's time to stop splitting up my branches?

## Footnotes

[^1]: This will be like a golf score, where a higher number is worse.

[^2]: By polynomial fit, we mean that some function $f = p_0 + p_1 x + p_2 x^2 + \cdots + p_n x^n$ will be estimated from training data. But this is from the topic of regression, which will be covered later.

[^3]: Using the term "smoothness" offers neither a complete nor an accurate definition, but I think that it's the most intuitive way of understanding the L2 norm. There's a little bit of math that can explain L2 more rigorously. Please don't let "smoothness" stick in your head. I'm sorry if it does.

[^4]: By the way, the value $\lambda$ is an example of a hyperparameter. The "hyper-" prefix makes it sound like a scary word. In reality, it just means that it's a parameter that isn't explicitly calcualted from the data. That means we just have to twiddle the value until our loss function satisfies us in splitting up our datasets.