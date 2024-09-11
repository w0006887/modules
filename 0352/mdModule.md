---
title: "Module 0352: Binary comparison"
author: Tak Auyeung
---
# Only "less-than" is needed

Because all other comparisons can be translated to less-than, possibly with the use of some logical operators, we are only concerned with less than in this module.

# Interpreted value

Given a bit pattern $x$ with $m$ bits, a C++ program can interpret the value as `int` (signed) or `unsigned`. The `unsigned` interpretation is simple because it is the default method of interpreting the value of a number (of any base):

$v_u(x,m) = \sum_{i=0}^{m-1} x_i2^i$

However, the `int` interpretation is a little more tricky. Congruent modulo $2^m$ helps to understand how a bit pattern can represent different values. However, it does not help determine exactly what value a bit pattern represents.

Two's complement is an operator that performs the same operation as arithmatic negation. However, it is not helpful to indicate the value represented by a bit pattern.

It is the decision that the range of values using signed interpretation of a bit pattern that is helpful. An $m$-bit pattern represents values from $-2^{m-1}$ to $2^{m-1}-1$. This range, combined with congruent modulo $2^m$, helps to determine that the signed (`int`) intepreted value of an $m$-bit pattern $x$ is as follows:

$v_s(x,m) = (\sum_{i=0}^{m-2} x_i 2^i) - x_{m-1}2^{m-1}$

As an exmaple consider the 4-bit pattern $1011_2$. $v_u(1011_2,4)=1+2+0+8=11$, whereas $v_s(1011_2,4)=1+2-8=-5$.

# `unsigned` less-than

In a binary subtraction of two $m$-bit patterns $x-y$, $t_m=1$ if and only if $v_u(x,m) < v_u(y,m)$ assuming $t_0=0$.

This can be proven as follows using proof by induction.

The base-case is when $m=1$. By definition $t_1 = b(x_0,y_0)+b(q_0,t_0)$. Since $t_0$ is part of the assumption, $b(q_0,t_0)$ has to be 0. This means $t_1 = b(x_0,y_0) = !x_0y_0$. This means $t_1 = 1$ if and only if $x_0=0 \wedge y_0=1$. This proves the base case.

The induction step assumes the theorem is true up to $m=k$. In other words, the assumption is $t_k=1$ if and only if $v_u(x,k) < v_u(y,k)$.

By the definition of $v_u$, $v_u(x,k+1) = x_{k}2^{k} + v_u(x,k)$, and likewise for $y$. In a $k+1$ bit subtraction of $v_u(x,k+1)-v_u(y,k+1)=x_{k}2^k + v_u(x,k) - y_k2^k - v_u(y,k)$.

If $x_k=y_k$, then $t_{k+1}=b(x_k,y_k)+b(x_k \oplus y_k,t_k)=b(0,t_k)=!0t_k=t_k$. This means that in this case, $t_{k+1}=1$ iff $t_k=1$, but it makes sense because the difference between $v_u(x,k+1)$ and $v_u(y,k+1)$ is $v_u(x,k)-v_u(y,k)$.

If $x_k=1 \wedge y_k=0$, then $v_u(x,k+1)>v_u(y,k+1)$, but $t_{k+1}=0$ in this case.

If $x_k=0 \wedge y_k=1$, then $t_{k+1}=b(0,1)+b(1,t_k)=1$, this also means that $v_u(x,k+1) < v_u(y,k+1) \Rightarrow t_{k+1}=1$.

Conversely, 

$\begin{align*}t_{k+1} &=1 \\ & \Leftrightarrow \\ (b(x_k,y_k)=1 & \vee b(x_k \oplus y_k, t_k)=1\end{align*}$ 

$b(x_k,y_k)=!x_ky_k=1$ if and only if $(x_k=0 \wedge y_k=1)$. This means $v_u(x,k+1) < v_u(y,k+1)$. 

On the other hand, $b(x_k \oplus y_k, t_k)=1$ if and only if $(!(x_k \oplus y_k)t_k = 1) \Leftrightarrow ((x_k=y_k) \wedge t_k)=1$. 

In order for $!(x_k \oplus y_k)$ to be true, $x_k=y_k$. This means $(v_u(x,k+1)-v_u(y,k+1) = v_u(x,k)-v_u(y,k)) \wedge t_k=1$. Using the induction assumption of $t_k=1 \Leftrightarrow v_u(x,k) < v_u(y,k)$, we can conclude that $v_u(x,k+1) < v_u(y,k+1)$.

This concludes the induction step of the proof by induction.

# (Signed) `int` less-than

Unlike `unsigned` where the actual difference of $x-y$ cannot be its own value when $v_u(x,m)<v_u(y,m)$, signed `int` can represent the actual difference of $x-y$ because of the ability to represent negative values. This means $x < y \Leftrightarrow (x-y) < 0$. In a $m$-bit pattern interpreted signed, bit $m-1$ is the sign bit. This means $d=x-y$, $d_{m-1}=1 \Leftrightarrow v_s(x,m) < v_s(y,m)$.

This works fine as long as the actual difference is within the range of an $m$-bit pattern interpreted signed. Assume $m=4$, $x=1100_2$ and $y=0101_2$. In this case, $v_s(x,4)=4-8=-4$, $v_s(y,4)=1+4=5$. As a result, the *actual* value of $v_s(x,4)-v_s(y,4)$ is $-5-4=-9$. However, -9 is out of the range of signed values that can be represented. 

Instead, $-9 \equiv_{2^4} -9+16=7$. $7$ has a binary representation of $0111_2$.

This "out of range" problem can also happen in the opposite direction. Consider $x=0111_2$, $y=1110_2$. In this example, $v_s(x,4)=1+2+4=7$, whereas $v_s(y,4)=2+4-8=-2$. The actual difference of $v_s(x)-v_s(y)$ is $7-(-2)=9$. However, 9 is out of the range of a 4-bit pattern interpreted signed. However, we know that $9 \equiv_{2^4} 9-16 = -7$. $-7 = -8+1$, and as a result, $v_s(1001_2,4)=1-8=-7$, meaning that $-7$ is represented as $1001_2$.

How "over the range" can the difference be? If we use the $m=4$ example, then in one direction, the most negative value of a difference is $-8-7=-15 \equiv_{2^4} -15+16 = 1$, and in the other direction, $7-(-8)=15 \equiv_{2^4} 15-16 = -1$. 

Whenever the difference of the signed interpreted values $v_s(x,m)-v_s(y,m)$ is out of range, the sign of the difference, $d_{m-1}$, is opposite of what it should be. Furthermore, to determine whether the difference of the signed interpreted values is out of range, we only need to check whether the sign of the minuend is opposite to *both* the signs of the subtrahend and the difference.

This is why the overflow flag is defined as $O=x_{m-1}!y_{m-1}!d_{m-1}+!x_{m-1}y_{m-1}d_{m-1}$. The overflow flag is 1 iff $v_s(x,m)-v_s(y,m)$ is out of range.

The overflow flag is really indicating whether the actual sign of the difference should be opposite to the one computed using binary subtraction. If we define $S=d_{m-1}$ (as a shorthand), then $S \oplus O$ is the correct sign of $v_s(x,m)-v_s(y,m)$.

If we define $L=S \oplus O$, then $L=1$ iff $v_s(x,m) < v_s(y,m)$.

# Exercise

Perform the following in binary subtraction using a bit-width of 3. Figure out all the rows, $x,y,q,t,d$, as well as the flags `B` (same as $t_3$) `S` (same as $d_2$), `O` (overflow), and `L` (less-than).

Note that the range of signed values given a width of 3 bits is from -4 to 3,and the unsigned values is from 0 to 7.

* 2-3
* -2-(-3)
* 3-2
* -2-3
* 2-(-3)
