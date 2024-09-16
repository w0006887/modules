---
title: "Module 0293: Aleph null"
---

# _{{ page.title }}_

# About this module

-   Prerequisites: [0290](../0290/mdModule.html), [0280](../0280/mdModule.html)

-   Objectives: This module discusses the special cardinality known as
    $\aleph_0$ and examples of how to map elements of one set to
    another.

# The set of natural numbers

The set of natural numbers, $\mathbb{N}$ is simple. It contains all the
non-negative integers, starting with 0. However, the cardinality of the
set of natural numbers has a special name: $|\mathbb{N}| = \aleph_0$.
One may think it makes no sense because the set of natural numbers has
an infinite number of elements, so why bother to give it a symbol?

# Equivalent cardinality

To understand the significance of $\aleph_0$, let us consider the set of
all integers, $\mathbb{Z}$. How does $|\mathbb{Z}|$ compare to
$|\mathbb{N}|$?

At first glance, the set of integers have more elements, after all, the
set of integers include all natural numbers and on top of that all
negative integers. However, as it turns out,
$|\mathbb{Z}| = |\mathbb{N}| = \aleph_0$.

How is this quality established?

Let us imagine there is a function
$f: \mathbb{Z} \rightarrow \mathbb{N}$ defined as follows:

$f(x) = (x \ge 0) ? (2x) : (-2x-1)$

In this function definition, I am using the ternary operator in C/C++.
This function maps all non-negative integers to even natural numbers,
and all negative integers to odd natural numbers.

Let us examine this function $f$ a little more. Is it injective? Given
two different integers from $\mathbb{Z}$, are they guaranteed to map to
different natural numbers? How do we prove this?

Let $p,q \in \mathbb{Z}$. There are four scenarios:

-   $p=q$, if this is the case, then we don't know have a problem with
    $f(p) = f(q)$.

-   $p \ne q$, one is negative, the other one is non-negative. According
    to the function $f$, one maps to an odd number while the other maps
    to an even number. As a result, $f(p) \ne f(q)$ is guaranteed.

-   $p \ne q$, both are non-negative. Algebra can be used to show that
    $p \ne q
              \Rightarrow 2p \ne 2q$, therefore $f(p) \ne f(q)$.

-   $p \ne q$, both are negative. Again, algebra can be used to show
    that $p \ne q \Rightarrow -2p \ne -2q \Rightarrow -2p+1 \ne -2q+1$.
    As a result, we also guarantee $f(p) \ne f(q)$.

Is this function $f$ surjective? In other words, can we guarantee that
all elements in $\mathbb{N}$ are mapped to?

The intuitive proof is to say that non-negative integers map to all the
even natural numbers, and negative integers map to all the odd natural
numbers. All natural numbers are either odd or even, so they are all
mapped.

However, a better and more rigorous proof is to prove that given any
natural number, there is an integer mapped to it. Let us consider
$x \in \mathtt{N}$.

-   $x$ is even. In this case, we know that the integer $\frac{x}{2}$
    maps to $x$.

-   $x$ is odd. In this case, we know that the integer $\frac{x+1}{-2}$
    maps to $x$.

Since $f$ is injective and surjective, it is bijective. There is an
inverse function $f^{-1}$, it can be defined as follows:

$f^{-1}(x) = (x \mod 2 = 0) ? \frac{x}{2} : \frac{x+1}{-2}$

Because $f$ is bijective, it follows that we can claim that $\mathbb{N}$
and $\mathbb{Z}$ have the same cardinality.

# Infinitely countable

The cardinality of $\mathbb{N}$ is infinite, however, it is also called
"countable". There are sets where the cardinality is not countable. For
example, the set of real numbers, $\mathtt{R}$, is not countable.

# What else is countable?

Surprisingly, the set of all 2-D coordinates using natural numbers is
also countable. This seems pretty odd because we are mapping a 2-D space
to a number line. Let us use $g$ to denote a function that maps 2-D
coordinates to natural numbers.

This is accomplished by filling a 2-D space (using only natural numbers
on both axes) in a diagonal way as follows:

-   $g((0,0)) = 0$

-   $g((1,0)) = 1$

-   $g((0,1)) = 2$

-   $g((2,0)) = 3$

-   $g((1,1)) = 4$

-   $g((0,2)) = 5$

-   $g((3,0)) = 6$

-   $g((2,1)) = 7$

-   $g((1,2)) = 8$

-   $g((0,3)) = 9$

-   \...

There is definitely a general pattern here. We are filling space with
diagonal lines that go from lower right to upper left. The first
diagonal "line" is just the coordinate (0,0). The second diagonal line
has two pixels, (1,0) and (0,1), the third has three pixels, (2,0),
(1,1) and (0,2) and so on.

Here is some observations. The length of diagonal lines increase by 1 as
we draw more lines to the upper right direction. The base of each
diagonal line is always in the form of $x,0$ where $x$ denotes the $x$th
diagonal line from the left margin, $x$ is zero indexed.

This gives us some clues to make a closed form of the function $g$.
First of all, we can figure out that:

$g((x,0)) = 0+1+2+3+4+\dots x$

This is nice, but we can do better:

$$\begin{aligned}
    g((x,0)) & =  0+1+2+3+\dots + (x) \\
             & =  \sum_{i=0}^{x} i \\
	     & =  (x \mod 2 \ne 0) ? &
	          (\sum_{i=0}^{\frac{x-1}{2}}{i}+ \sum_{i=\frac{x-1}{2}+1}^{x}{i}) & : 
	           (\sum_{i=0}^{\frac{x}{2}-1}{i} + \sum_{i=\frac{x}{2}+1}^{x}{i} + {\frac{x}{2}} ) \\
	     & =  (x \mod 2 \ne 0) ? &
	          (\sum_{i=0}^{\frac{x-1}{2}}{(i+(x-i))}) & : 
	           (\sum_{i=0}^{\frac{x}{2}-1}{(i+(x-i))} + {\frac{x}{2}} ) \\
	     & =  (x \mod 2 \ne 0) ? &
	          (\sum_{i=0}^{\frac{x-1}{2}}{(x))}) & : 
	           (\sum_{i=0}^{\frac{x}{2}-1}{(i+(x-i))} + {\frac{x}{2}} ) \\
	     & =  (x \mod 2 \ne 0) ? &
	          ((\frac{x-1}{2}+1){(x))}) & : 
	           ((\frac{x}{2}){(x))} + {\frac{x}{2}} ) \\
	     & =  (x \mod 2 \ne 0) ? &
	          ((\frac{x-1+2}{2})x) & : 
	           (\frac{x}{2}x + {\frac{x}{2}} ) \\
	     & =  (x \mod 2 \ne 0) ? &
	          (\frac{x(x+1)}{2}) & : 
	           (\frac{x}{2}(x+1)  ) \\
	     & =  (x \mod 2 \ne 0) ? &
	          (\frac{x(x+1)}{2}) & : 
	           (\frac{x(x+1)}{2}  ) \\
	     & =  \frac{x(x+1)}{2} 
  
\end{aligned}$$

Now that we know how to get $g$ computed for all the pixels at the base
of all the diagonal lines, how do we compute the $g$ value of the other
pixels?

We do know that we are counting from the base of a diagonal line to the
upper left direction. Assuming the coordinate of the pixel is (x,y), the
base of this pixel is at (x+y,0). This is because the y coordinate is
the same as the x-offset from the base pixel of a diagonal line.

We can name define an notaion,
$D(n)=\{(x,y)|(x \in \mathbb{N}) \wedge (y \in \mathbb{N}) \wedge (n=x+y)\}$.
Diagonal line $D(n)$ is a set of two tuples where the individual
components of each two tuple add up to the value of $n$.

This means the base number of the pixel at (x,y) is
$\frac{(x+y)(x+y+1)}{2}$. But this is just the $g$ value of the base of
diagonal line $D(x+y)$. Since the pixel (x,y) is y pixels from the base,
the actual $g((x,y)) = \frac{(x+y)(x+y+1)}{2}+y$.

Whew, that was a rather long derivation! Zooming out of the details, let
us reexamine the significance of function
$g: \mathbb{N}\times \mathbb{N} \rightarrow \mathbb{N}$. It is a
function that maps all discrete pixels of a 2-D space to natural
numbers. Immediately we know the cardinality of
$\mathbb{N}\times \mathbb{N}$ is not more than $\aleph_0$! If we can
prove that $g$ is injective and surjection, then we know that
$|\mathbb{N}\times \mathbb{N}| = |\mathbb{N}| = \aleph_0$, and that is
just awesome!

Intuitively, we now $g$ is injective. Because of the way the diagonal
lines "sweep" in only one direction, no two pixels can map to the same
natural number. Of course, this is not a very rigorous proof.
Nonetheless, it makes sense.

Surjectiveness, on the other hand, is a little more troublesome to
prove. We need to prove that for every natural number, there is a pixel
in the discrete 2-D space that maps to it.

Again, intuitively, it makes sense. After all, we can use the sweeping
action to fill diagonal lines until we reach the given natural number.

Our new challenge is then to find $x$ and $y$ so that for a given
natural number $n$, $g((x,y)) = n$. In other words, we are looking for
$g^{-1}$, the inverse function.

To find the inverse function, we first have to find the diagonal line,
then the position of the pixel on the diagonal line. Symbolically, given
that $g^{-1}(n) = (x,y)$, we are trying to find a $w$ such that $w=x+y$.
We can form the following relationship:

$g((w,0)) = \frac{w(w+1)}{2} \le n$

Then we perform some algebra operations:

$$\begin{aligned}
  \frac{w(w+1)}{2} & \le n \\
    \frac{w^2}{2} + \frac{w}{2} & \le n \\
    0.5w^2 + 0.5w - n  & \le 0 \\
    w^2 + w - 2n & \le 0
  
\end{aligned}$$

Ignoring that this is an inequality, we can solve for $w$ as if it is a
quadratic *equation*.

$w = \frac{-(1) \pm \sqrt{(1)^2 - 4(1)(-2n)} }{2\cdot 1}$

Since we know
$x \in \mathbb{N} \wedge y \in \mathbb{N} \Rightarrow (w=x+y)
  \in \mathbb{N}$, we conclude with the following:

$w = \lfloor \frac{\sqrt{8n+1}-1}{2} \rfloor$

Once $w$ is solved, the rest is rather easy. First of all,

$$\begin{aligned}
     n = g((x,y)) & = \frac{(x+y)(x+y+1)}{2} + y \\
                  & = \frac{w(w+1)}{2} + y \\
                y & = n - \frac{w(w+1)}{2}
  
\end{aligned}$$

With $y$ computed, $x = w-y$. We have the coordinate solved!

To connect all the pieces, let us define:

$w(n) = \lfloor \frac{\sqrt{8n+1}-1}{2} \rfloor$

Then we can use the fact that $g((w(n),0)) = \frac{w(n)(w(n)+1)}{2}$.
The y component of the solution is then $y(n) = n - g((w(n),0))$,
wherease the x component is
$x(n) = w(n) - y(n) = w(n) - n + \frac{w(n)(w(n)+1)}{2}$.

The final answer is, as a result:

$$\begin{aligned}
    g^{-1}(n) & = \bigl ( x(n), y(n) \bigr ) \\
              & = \bigl ( \frac{w(n)(w(n)+3)}{2} - n, n - \frac{w(n)(w(n)+1)}{2} \bigr )
  
\end{aligned}$$

There is no doubt that this is a rather long derivation, but the result
is rather interesting. After all, we show that
$|\mathbb{N} \times \mathbb{N}| = | \mathbb{N} | = \aleph_0$!

Does this pair of functions, $g$ and $g^{-1}$ have any practical use?

Besides illustrating the concept of $\aleph_0$ and infinite but
countable sets, this 2D to 1D folding mechanism can potentially be
useful for the transmission of data. This mechanism essentially
illustrates any number of integers can be encoded as a single integer.
