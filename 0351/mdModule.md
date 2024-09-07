---
title: Module 0351: Signed vs unsigned integer representation 
---

# _Module 0351: Signed vs unsigned integer representation_

# Finite bit-width

Although the set of integers (math symbol $\mathbb{Z}$) has an infinite number of elements, the way an integer value is store in a computer has a finite bit-width. And with that, a finite range of values to be represented.

Based on the discussion of how values are represented by numbers in [module 0282](../0282/mdModule.html), a base-2 number with digits 0 to ${w-1}$ (therefore a total of $w$ digits, $w$ is an integer that is at least 1) can represent values from 0 to $2^{w}-1$

For example, given only a width of 4 bits, integer values from 0 to $2^4-1=15$ can be represented.

But then what about the other integer values? For example, how is 19 represented?

## A tricky answer

There are two ways to look at the question of how 19 is represented as a 4-bit integer. The first one is simply to say that 19 cannot be represented as a 4-bit integer. This interpretation is relevant and useful in most cases.

However, an alternative to look at this is that 19 has the same representation as 3 as a 4-bit integer. This is based on congruent modulo between 3 and 19. You can visit the [Wikipedia page](https://en.wikipedia.org/wiki/Modular_arithmetic) for a more complete treatment of this subject matter.

In this context, however, we are only interested in the basic definition. The following are boolean expressions, and they are equivalent:

* $a \equiv b (\mod n)$: this notation is used in the Wikipedia page and most textbooks
* $a \equiv_n b$: this is Tak's lazier notation
* $(a = v + k_a \cdot n) \wedge (b = v + k_b \cdot n)$ for some integers $k_a$ and $k_b$, and some integer $v$ such that $0 \le v < n$.

In all these definitions, $n$ is an integer that is at least 2.

Let us reconsider our example, $3 \equiv_{16} 19$. This is because $v=3$, then $3=3+0\cdot 16$ and $19=3+1\cdot 16$. In English, you can say "3 and 19 are congruent modulo 16."

## But why is congruent modulo important?

Sure, trying to interpret $0011_2$ as 3 or 19 *is* silly. However, congruent modulo helps answer a more useful question: how do we represent negative values in base 2?

# Negative integers

Recall that $a \equiv_n b$ is the same as saying 
$(a = v + k_a \cdot n) \wedge (b = v + k_b \cdot n)$ for some integers $k_a$ and $k_b$, and some integer $v$ such that $0 \le v < n$. There is no restriction whether $k_a$ and $k_b$ can be negative! 

This means that in general, for any base, a negative and a non-negative value can be congruent modulo $n$. For exmaple, using $n=16$,  3 and -29 are congruent modulo 16. This is because $3=3+0\cdot 16$, and $-29=3+-2\cdot 16$. 

-29 is too far on the negative side to be represented. This is because the multiplier to 16 is -2. However, if the multiplier is just -1, we can *potentially* use congruent modulo 16 to represent negative values.

Let us example the following congruent modulo 16 table.

|$v$|$k_a$|$a$|$k_b$|$b$|
|-|-|---|-|---|
|0|0|0|-1|-16|
|1|0|1|-1|-15|
|2|0|2|-1|-14|
|3|0|3|-1|-13|
|4|0|4|-1|-12|
|5|0|5|-1|-11|
|6|0|6|-1|-10|
|7|0|7|-1|-9|
|8|0|8|-1|-8|
|9|0|9|-1|-7|
|10|0|10|-1|-6|
|11|0|11|-1|-5|
|12|0|12|-1|-4|
|13|0|13|-1|-3|
|14|0|14|-1|-2|
|15|0|15|-1|-1|

In C++, the `unsigned` type uses $k_a=0$, and that is fairly easy to understand. However, the `int` type, on the other hand, cannot *just* use $k_b=-1$ because otherwise an `int` can only represent negative values!

The "balance" is that for an `int`, half the values are non-negative, and the other half are negative. In the examples of a 4-bit integer, 0 to 7 are the non-negative ($k_a=0$) values, and -1 to -8 are the negative ($k_b=-1$) values. 

Generally speaking, given a $w$-bit integer, the range of `unsigned` values is $0$ to $2^{w}-1$, the range of `int` (signed integer) values is $-2^{w-1}$ to $2^{w-1}-1$.

Assume $w=4$, resulting in $n=2^w=16$, and convert all the $a$ values in range of `int` (signed integer) to 4-bit binary numbers. Also observe the pattern for binary numbers representing negative values (as $b$) that are in `int` range as described in the previous paragraph? Furthermore, what is a good name for bit 3 in this specific case?

# Arithmetic negation in base-2

The following is true regardless of $n$:

$-v \equiv_n -v + k\cdot n$ 

by the definition of congruent modulo $n$. That said, let us consider a much more specific case when $k=1$: $-v \equiv_n -v + n = -v + ((n-1)+1) = ((n-1)-v)+1$. The bottom line is that $-v \equiv_n ((n-1)-v)+1$ for any $n$.

But why is this significant? Well, it is significant *specifically* in the case when $n=2^w$ for some integer $w>0$. Assuming $n=2^w$, then $-v \equiv_{2^w} ((2^w-1)-v)+1$.

It helps to use an example. Let $w=4$, and $v=3$. Then $-3 \equiv_{16} ((16-1)-3)+1$. The trick is how we look at $((16-1)-3)$. Obviously, it is the same as $15-3$. Let's example the base-2 representations: $15=1111_2$, and $3=0011_2$.

In fact, it is true that for all $w>1$, the binary representation of $2^w-1$ consists of $w$ contiguous 1's! In the [binary subtraction module](../0284/mdModule.html), we learn that $t_{i+1}=b(x_i,y_i)+b(q_i,k_i)=!x_iy_i + !(x_i \oplus y_i)t_i$. If $x_i$ is guaranteed a 1, and the initial $t_0=0$, then we can prove (using proof by induction) that $t_i=0$ for the entire $t$ row.

In fact, for each digit in this specific case (when $x_i=1$), $q_i = x_i \oplus y_i= 1\oplus y_i= !y_i$, and since $t_i=0$, $d_i = q_i \oplus t_i = q_i \oplus 0 = q_i = !y_i$. You can proof that for any boolean value $k$, $k \oplus 0=k$, and $k \oplus 1=!k$

Because each bit of the difference is just a logical not of the subtrahend, we can say that the difference is a bitwise-not of the subtrahend. In C++ operator, we confirm that `d == ~y`. 

You should verify this observation and write some code in C++ or use a debugger to confirm. 

Now we can plug this into the original congruent modulo $n$ statement: $-v \equiv_{2^w} ((2^w-1)-v)+1 = \sim v+1$. This is called the two's complement because one's complement is $\mathrm{C1}(x) = \sim x$ (same as bitwise-not), and then $\mathrm{C2}(x)=\mathrm{C1}(x)+1$.

Two's complement is important because it is a way to perform arithmetic negation using bitwise-not and addition of 1. Let's check out two examples:

How is -3 represented as a signed 4-bit integer? $3=0011_2$, $-3=\mathrm{C2}(0011_2)=\mathrm{C1}(0011_2)+1=1100_2+1=1101_2$. This is consistent the table that we have!

Then what is -(-3)? $-(-3) \equiv_{16} \mathrm{C2}(1101_2)=\mathrm{C1}(1101_2)+1=0010_2+1=0011_2$. Indeed, $-(-3)=3$!

# But wait, is `1101(2)` 13 or -3?

From a [previous module discussion how a value is represented by a number](../0282/mdModule.html), we know that $1101_2$ represents the value of 13. But now we claim that the same bit-pattern (binary number) also represents -3. So which one is it?

The answer is "it depends."

What $1101_2$ represents depends on how the bit pattern is used. For example, if $1101_2$ is the content of some video RAM of a monochrome display card (circa 1981) in graphics mode, then it represents two pixels, one in full brightness, and the other one at $\frac{2}{3}$ brightness.

*Until* a bit pattern is actually utilized, it has no inherent meaning or interpretation. 

This means that the bit pattern $1101_2$ represents -3 only when the bit pattern is supposed to represent a signed 4-bit integer. The same bit pattern represents 13 only when the bit pattern is supposed to represent an unsigned 4-bit integer.

Note that even binary addition and subtraction do not care about sign interpretation. $1101_2+0001_2=1110_2$ works for $-3+1=-2$ as well as $13+1=14$.
