---
title: "Representing a Line Between Two Points with Homogeneous Coordinates (An Intuitive Representation)"
date: 2026-10-01
excerpt: "Why does A + λB describe the line through two homogeneous points? A geometric and algebraic look at how dividing by the last coordinate recovers the familiar (1 − t)Ã + tB̃."
tags:
  - computer vision
---


Hello! Today I am writing my first post, inspired by the great series of
mathematics posts by [Gregory Gundersen](https://gregorygundersen.com/blog/2020/01/12/why-research-blog/). Today I will be talking about some
properties of homogeneous coordinates in the context of computer vision that
were extremely confusing to me in the beginning.

In this post, we will decipher the enigmatic parametric representation of a
line between two points in homogeneous coordinates. To make this more concrete,
we will understand why, if we have two homogeneous points $$A$$ and $$B$$, any
other point in between them can be represented with

$$
X(\lambda) = A + \lambda B
$$

If you think about this from a normal (non-homogeneous) geometry perspective,
you should feel, like me, uncomfortable about the fact that the expression above
describes the points on the line between the anchor points.

The usual way I was taught to parametrize a line was

$$
\tilde{X}(t) = \tilde{p}_0 + t\,\tilde{d}
$$

where $$\tilde{p}_0$$ is a point that the line passes through and $$\tilde{d}$$
is a direction vector. Now, if you had two non-homogeneous points
$$\tilde{A}$$ and $$\tilde{B}$$, the line passing through the two points would be

$$
\tilde{X}(t) = \tilde{A} + t(\tilde{B} - \tilde{A}) = (1 - t)\tilde{A} + t\tilde{B}
$$

Here, we will reconcile the homogeneous and non-homogeneous parametrizations of
the line between two points. As a note, this representation appears
extensively in many proofs and explanations in computer vision classes, so it
is a very useful concept to have.

## Background

If you have never worked with homogeneous coordinates, please don't expect an
extensive study of this mathematical tool. Here, I assume my readers have had
some exposure to the world of projective geometry and homogeneous
coordinates in the context of computer vision. For beginners interested in a
complete resource on the topic, I would recommend the first hand-written notes
from Professor Avinash Kak [here](https://engineering.purdue.edu/kak/computervision/) (not beginner-friendly material, but material
that will give you the basics and get you back to this post to appreciate it
more).

The only thing that I will include for the sake of completeness is that, in
homogeneous coordinates, vectors get converted by adding an additional
dimension. This means that the information of the vector will now be 
contained in the ratio of the numbers. This last property means that all
homogeneous entities are invariant to multiplication by a non-zero scalar.

So, for instance, the 2D vector $$\tilde{X} = [x_1, x_2]$$ can be represented
in homogeneous coordinates by $$X = [x_1, x_2, 1]$$. Additionally, we have that
$$X \sim aX$$, where $$a$$ can be any non-zero scalar and $$\sim$$ denotes
equivalence (both vectors represent the same point).  To recover the encoded 2D vector from the homogeneous representation,
it is just necessary to divide all the components of the vector by $$x_3$$:

$$
X = [x_1, x_2, x_3] \sim \left[\frac{x_1}{x_3}, \frac{x_2}{x_3}, \frac{x_3}{x_3}\right] = \left[\frac{x_1}{x_3}, \frac{x_2}{x_3}, 1\right]
$$

Notice the notation we will follow from now on: non-homogeneous points will be
represented with $$\tilde{X}$$, while the homogeneous representation will be
$$X$$.

## The geometric explanation

To analyze the behavior of the homogeneous line parametrization, let's observe
the figure below. Here, we build three lines ($$l_1$$, $$l_2$$, and $$l_3$$)
using the base vectors $$\tilde{A}$$ and $$\tilde{B}$$. Our geometric intuition
should tell us that, for instance, the line

$$
l_1 = \tilde{A} + t\tilde{B}
$$

represents the line that goes through the point $$\tilde{A}$$ and has the
direction of $$\tilde{B}$$. Now, if we were to upgrade this operation to
homogeneous vectors,

$$
l_3 = A + tB
$$

the line represented by this equation will change. The key to understanding
this difference lies in how we recover the 2D vectors represented by their
homogeneous counterparts, which requires dividing by the last component of the
vector. This division rescales the vectors so that they land on the line
$$l_3$$.

![Geometric understanding of the parametrization of a line between two points]({{ "/images/blog/plot_for_hc_lines.png" | relative_url }})

The two green lines in the figure represent the points $$\tilde{A} + 2\tilde{B}$$
and $$2\tilde{A} + \tilde{B}$$, which clearly don't land on our line $$l_3$$.
However, performing the homogeneous counterpart of this operation and then
dividing by the last component of the vector will lead to vectors landing on the
line $$l_3$$.

## The algebraic explanation

Algebraically, it is simple to demonstrate why the green vectors in our previous
figure land on the line $$l_3$$. This understanding comes from observing what happens to the last dimension of
the vectors involved. For simplicity, we will work with 2D homogeneous vectors $$A$$ and $$B$$ and assume
both of them have their third coordinate equal to 1, that is,
$$A = [a_1, a_2, 1]$$ and $$B = [b_1, b_2, 1]$$.

Starting with

$$
X(\lambda) = A + \lambda B
$$

This can be written as

$$
X(\lambda) = [a_1 + \lambda b_1, \; a_2 + \lambda b_2, \; 1 + \lambda]
$$

Since we only care about ratios in the vector, this turns into

$$
X(\lambda) \sim \left[\frac{a_1 + \lambda b_1}{1 + \lambda}, \; \frac{a_2 + \lambda b_2}{1 + \lambda}, \; 1\right]
$$

Then, by doing the parameter substitution

$$
t = \frac{\lambda}{1 + \lambda}
$$

and keeping in mind that

$$
1 - t = \frac{1}{1 + \lambda}
$$

you can convert the expression above into the following non-homogeneous equation:

$$
\tilde{A}(1 - t) + t\tilde{B} = \tilde{A} + (\tilde{B} - \tilde{A})t
$$

$$
\tilde{X}(t) = (1 - t)\tilde{A} + t\tilde{B}
$$

## Conclusions

I will close this post with the following two conclusions. First, the
homogeneous representation leads to a compact representation of the line
between two points that differs from the usual parametrization in
non-homogeneous coordinates. Second, whenever you are looking at an equation in
computer vision, keep in mind how your vectors are represented, as it can
significantly change the interpretation of the math.
