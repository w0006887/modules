# _Module 0288: Set notations defined using quantifiers_

# About this module

-   Prerequisites: [0280](../0280/mdModule.html), [0285](../0285/mdModule.html)

-   Objectives: Set theory using quantifiers

# Rationale

Although basic set theory was already discussed in module
[0280](../0280/mdModule.html), that was discussed without the use of quantifiers.
Quantifiers are useful tools for a variety of math topics, set theory is
a part of those topics. By reexamining basic set theory, we reinforce
the understanding of both set theory as well as quantifiers.

# Equality

Given two items, $x$ and $y$, how do we know they are the same? In order
words, how do we evaluate $x=y$?

First of all, if one is a set and other is not, then $x=y$ is false.

Given that $x$ and $y$ are not sets, then the "normal" comparison
applies.

Given that $x$ and $y$ are sets, then we can say the following:

$(x=y) \Leftrightarrow ((\forall e \in x(e \in y)) \wedge (\forall e \in y(e \in x)))$

There is a more concise statement that states the same:

<span id="setEquality">$(x=y) \Leftrightarrow (\forall e((e \in x) \Leftrightarrow (e \in y)))$</span>

# Set description

Recall the notation $E=\\{x|P(x)\\}$ describes a set $E$ where all its
elements make the predicate $P$ true. We mentioned how this means
$x \in E \Leftrightarrow
  P(x)$ in module [0280](../0280). The more correct statement is as
follows:

$\forall x(x \in E \Leftrightarrow P(x))$

This makes it clear where we get (how we bind) the value of the variable
to some "thing." $x$ can be anything in the universe! Without the
quantifier $\forall$, one can ask the question where do we get a value
for $x$ to be evaluated.

# The empty set

How do we know that a set $S$ is empty?

$\neg \exists x(x \in S)$

This literally says "there does not exist a thing $x$ such that $x$ is
in $S$."

# Intersection and Union

$\forall x((x \in (A \cap B)) \Leftrightarrow (x \in A \wedge x \in B))$

and

$\forall x((x \in (A \cup B)) \Leftrightarrow (x \in A \vee x \in B))$

# Cartesian product

$\forall x \in A(\forall y \in B((x,y) \in (A \times B))) \wedge \forall (x,y) \in A \times B(x \in A \wedge y \in B)$

# Subset

$A \subseteq B \Leftrightarrow \forall e \in A(e \in B)$

$A \subset B \Leftrightarrow (A \subseteq B \wedge \exists x \in B(\neg x \in A))$
