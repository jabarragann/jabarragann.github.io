---
title: "Representing a line with Homogeneous Coordinates (An unintuitive representation"
date: 2026-10-01
excerpt: "Coming soon."
tags:
  - robotics
  - computer graphics
  - math
---


Hello, today I am writing my first poster inspired by the great series of
mathematics posts by [PENDING](). So, today I will be talking about some
properties of homogenous coordinates in the context of computer vision that
were extremely confusing for me in the beginning. 

Today, we will decipher the enimatic parametric representation of lines in
homogenous of coordinates.

$$ X(lambda) = A + lambda * B $$

where X represents the points on the line between A and B. If you think about
this from normal geometry perspective you should feel like me uncomfortable about hte
fact that the expression above describe the points on the line between the
ancher points.

The usual way I was taught to parametrize a line was by 

$$ ~x(t) = a + t (dir) $$

where a is a point that the line passes by and the $dir$ is a direction vector.
Now if you had to non-homogenous points $~a$ and $~b$, the line representing
two points would be 

$$ ~x(t) = a + t (b-a)  = (1-t) a + t b $$

In here we will reconciliate the non-intuitive representation in of a line
between two homoegnoeus points. As a note this representation appears
extensively in many proofs and explanation in computer vision classes so it is
a very useful concept to have in mind.

## Background

If you have never worked with homogenous coordinates, please don't expect an
extensive study of this mathematical tool. In here my target audience are
people who have had some exposure to the world projective geometry and homogenous
coordinates in the context of computer vision. For people interested in a complete
resource about the topic, I would recommended the first hand-written notes from
Professor Avisah Kak in here (Not a beginners friendly material but a material
that will give the basics get you back to this post to appreciate it more).

The only thing that I will include for the sake of completeness is that in
homogenous coordinates vectors get converted by adding an additional dimension
to them and by keeping in mind the intepretation that information is contained
in the ratio of the numbers. This last property means that all homegeonous
entities are invariant to scalar multiplicative scalars. 

so for instance the 2D vector $$ ~x = [x1, x2]$$ can be represented to homogenous coordinates
by $$X =[x1,x2,1] $$ and that $$X = aX$$ where a can be any non-zero scalar.
Notice the notation we will follow form this on. Non homogenous points will be
represented with $~x$ while homogeonous representastion will be $x$.

## The geometric explanation

## The algebraic explanation

So algebraically is very simple to reconciliate both our line representations.
Given points A and B, it is easy to see why the homogenous representation leads to
a compact representation for the line between two points by following what happens
to the last dimension of the vector. For simplicity we will work in 2d homogenous vectors.

Starting with 
$$
X(lambda) = A + lamda B
$$

This can be written as 

$$
X(lambda ) = vector [a1 + lambda b1, ...  , .... ]
$$

Since we only care about ratios in the vector this turns into 
$$
X(lambda) = vector[a1+ lambda/(1+lambda), ... ,...]
$$

Then by doing the parameter substitution of

$$
t = lambda/(1+lambda) 
$$

and keeping in mind that 

$$
(1-t) = 1 /(a+lambda)
$$

you can convert the expresion above as 

$$
~A(1-t) + t ~b = ~a + (~b-~a) * t
$$


$$x(t) = (1 - t)a + t *b $$
