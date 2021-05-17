---  
title: "Deriving Ambisonics (pt. 1)"
custom_title: true
nav_order: 3
parent: Literature
---
<center>
<h1>Taking the Ambiguity out of Ambisonics</h1>
<h3>Part 1: The Wave Equation</h3>
</center>

This is a dump of some of my thoughts as I try to wrap my mind around Ambisonics in a more intuitive way, particularly its derivation of the spherical harmonics used in the Ambisonic domain. It is structured as a conversation, with series of questions and answers.

## Question 1: How do we represent a moving wavefront in three-dimensional space?

This is probably the most central question that is asked whenever dealing with spatial audio technologies.

First, let us describe a wave in the first place. At its most basic, the linear behavior of a wave can be described by the wave equation. It was probably figured out by some really observant people dropping pebbles in ponds and swinging ropes and springs with fixed ends. We will call this a governing equation because it *governs* our exploration. In other words, it acts like a constraint: no matter how deep we get into representing acousatic events, it must follow the relationship of this equation.
### Wave Equation
The wave equation looks like this:

$$
\frac{\delta^2 u}{\delta t^2} = c^2\frac{\delta^2 u}{\delta x^2}
$$

There is no need to find an explicit solution at this point -- that fact alone takes a great deal of confusion out of my mind. Here's how I parse through the wave equation.

#### 1. Let's look at the variables.
Whenever we see a tough equation, we just need to know that it describes a relationship between variables. In the case of the wave equation, there's some relationship between a particle's velocity $u$, time $t$, and position $x$. The speed of the particle in a medium $c$ will be regarded as a constant. Now what exactly is this relationship?

#### 2. Let's look at the operators.
Whenever we see deltas $\delta$ arranged like a fraction, they describe the change of a quantity with respect to change of another variable. It may help to look at it like this:

$$
\frac{\delta^2}{\delta t^2}\Big(u\Big) = c^2\frac{\delta^2}{\delta x^2}\Big(u\Big)
$$

Now, we can see that if you look at the double derivative of a particle's velocity $u$ with respect to time $t$, it will behave the same way as the double derivative of its velocity with respect to displacement. In other words, whether you look at it over time or if you freeze to an instant of time and look at it across space, it will look the same.
