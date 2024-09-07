---
title: "Module 0290: Injection, Surjection and Bijection"
---

# _{{ page.title }}_

# About this module

-   Prerequisites: [0289](../0289/mdModule.html)

-   Objectives: This module explores categories of functions known as
    injection, surjection, and bijection, as well as the implications of
    these categories.

# Injection

An injective function, aka an injection, has each element of the domain
mapped to a unique element in the codomain. Let us assume the function
of interest is $f: X \rightarrow Y$. Then an injection has the following
additional property (this statement is true):

$\forall p \in X(\forall q \in X((p \ne q) \Rightarrow f(p) \ne f(q)))$

Or it can also be stated as follows counting the number of elements in
the domain that can map to an element in the codomain:

$$\forall q \in Y(|\{(p,q)|(p,q) \in f\}| \le 1)$$

Let's examine some examples where $f: \\{a,b\\} \rightarrow \\{1,2,3\\}$:

-   $f=\\{(a,2), (a,1)\\}$: this set $f$ is not even a function!

-   $f=\\{(a,1), (b,1)\\}$: two things maps to 1, leaving the other
    element in $X$.

-   $f=\\{(a,1), (b,2)\\}$: this is injective despite having an element in
    Y that is not used.

# Surjection

A surjective function, aka a surjection, is a function where every
element in the codomain is mapped to. The following statement is true
for a surjection $f: X \rightarrow  Y$ in addition to the requirement of
being a function:

$\forall q \in Y(\exists p \in X(f(p)=q))$

Or alternatively, by counting:

$$\forall q \in Y(|\{(p,q)|(p,q) \in f\}| \ge 1)$$

Let's re-examine the assumption that $f: \\{a,b\\} \rightarrow \\{1,2,3\\}$.
Well, any function $f$ like this cannot be surjective! This is because
there are more elements in the codomain than there are elements in the
domain. In order for $f$ to be a function, each element in the domain
must map to one and only one element in the codomain!

We can change our domain so that $f: \\{a,b\\} \rightarrow \\{1,2\\}$. Now
we can examine a few examples:

-   $f=\\{(a,1),(b,2)\\}$ is surjective.

-   $f=\\{(a,1),(b,1)\\}$ is not surjective.

# Bijection

A bijective function, aka a bijection, is a function that is both
injective and surjective.

In other words, for a function $f: X \rightarrow Y$, we want

$$\forall q \in Y(|\{(p,q)|(p,q) \in f\}| \le 1)$$

and

$$\forall q \in Y(|\{(p,q)|(p,q) \in f\}| \ge 1)$$

But that means

$$\forall q \in Y(|\{(p,q)|(p,q) \in f\}| = 1)$$

Bijection is important because it implies reversibility. A function that
is bijective has an inverse.

# Inverse

A bijection is reversible. In other words, given a bijection
$f: X \rightarrow Y$, there is another bijection
$f^{-1}: Y \rightarrow X$ such that $\forall e \in X(f^{-1}(f(e)) = e)$
and $\forall e \in Y(f(f^{-1}(e)) = e)$.

But can we prove this?

Let's examine what we know about a bijection $f:X \rightarrow Y$.
Because a bijection is a function, we know the following is true:

$$\forall p \in X(|\{(p,q)|(p,q) \in f\}| = 1)$$

This is a requirement of all functions, that every element in the domain
be mapped to exactly one item in the codomain.

However, since we also assume $f$ to be a bijection, we also know that

$$\forall q \in Y(|\{(p,q)|(p,q) \in f\}| = 1)$$

As a result, if we define $f^{-1}$ so that

$\forall p \in X(\forall q \in Y(((p,q) \in f) \Leftrightarrow ((q,p) \in f^{-1})))$

Then by symmetry,

$$\forall q \in Y(|\{(p,q)|(p,q) \in f\}| = 1)$$

implies

$$\forall q \in Y(|\{(q,p)|(q,p) \in f^{-1}\}| = 1)$$

But this pattern means $f^{-1}$ is a function because all elements in
the domain of $f^{-1}$ are mapped to one thing in the codomain.

Likewise, the function property of $f$

$$\forall p \in X(|\{(p,q)|(p,q) \in f\}| = 1)$$

means

$$\forall p \in X(|\{(q,p)|(q,p) \in f^{-1}\}| = 1)$$

But this pattern means $f^{-1}$ is a bijection.

This concludes the proof that every bijection has a matching inverse
function.

## The sorting example

Recall at the end of module [0289](../0289/mdModule.html), we attempted to express the
correct outcome of a sorting algorithm. The problem that we were having
was due to the function $f$ can potentially map every index to one
single index. Now that we understand the concept of bijection, we can
specify that function $f$ must be a bijection.

This ensures that each initial value of the array elements is found in
one element of the array when the algorithm is finished.
