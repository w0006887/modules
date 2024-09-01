# _Module 0283: Binary Adition and Subtraction_

# Addition

## Base-10

### Example

| |3|2|1|0|digit position|
|-|-|-|-|-|--------------|
| | |7|5|2| $x$ |
|+| |2|4|9| $y$ |
|-|-|-|-|-|-|
| | |9|9|1| $q$ |
|+|1|1|1|0| $k$ |
|-|-|-|-|-|-|
| | |0|0|1| $s$ |


     3 2 1 0 digit
       7 5 2 x
    +  2 4 9 y
    --------
       9 9 1 q
    +1 1 1 0 k
    --------
       0 0 1

### Pattern extraction and Generalization

$x$ and $y$ are the numbers being added. $s$ is the sum. $q$ is an intermediate row, we call it the "single-digit sum of $x$ and $y$". $k$ is also an intermediate row, it is the *k*arry to a specific digit. $s$ turns out to be the single-digit sum of $q$ and $k$.

The concept of a single-digit sum is important when we need to computer multi-digit addition. This is because instead of viewing $5+7$ as $12$, we say that the single-digit sum is $2$ with a carry of $1$ to the digit to the right. This is because $5+7$ results in a value that cannot be represented by a single digit in base 10. This causes a carry of 1 to the next digit (which specifies a power of 10 that is 10 times of current column). Once the $10$ is taken care of using a carry, the "leftover" amount is $2$.

We define two functions. Assuming $u$ and $v$ are single base-10 digits, then $r(u,v)$ computes the single-digit sum, while $c(u,v)$ computes the carry. Following the logic of the previous paragraph, we can conclude that $r(u,v)=(u+v) \mod 10$, and $c(u,v)=(u+v \ge 10)?1:0$. Or, in C:

```c
unsigned r(unsigned u, unsigned v)
{
  return (u+v)%10;
}

unsigned c(unsigned u, unsigned v)
{
  return (u+v>=10) ? 1 : 0;
}
```

Based on these functions, we can now relate the digits based on their rows and columns. $q_i = r(x_i,y_i)$, $s_i = r(q_i, k_i)$, and $k_{i+1}=c(x_i,y_i)+c(q_i,k_i)$. 

## Base-2

### r and c, redefined

Based on [a previous section](#pattern-extraction-and-generalization), the functions $r$ and $c$ can easily be redefined for any base $b$. This is because the concept of a single-digit sum and carry is not base-dependent. Given that $b$ is the base, $r(u,v)=(u+v) \mod b$, and $c(u,v)=(u+v \ge b)?1:0$.

To work in base-2, $b=2$, this means $r(u,v)=(u+v) \mod 2$ and $c(u,v)=(u+v \ge 2)?1:0$. The relationship between the digits remain the same.

Let us first example all the possibilities of $c(u,v)$ in base-2:

|u|v|c(u,v)|
|-|-|-|
|0|0|0|
|0|1|0|
|1|0|0|
|1|1|1|

Does this look familiar? Indeed, in base-2, $c(u,v) = u \wedge v$, or in C, 

```c
unsigned c(unsigned u, unsigned v)
{
  return (u && v) ? 1 : 0;
}
```

This is convenient, because we know that conjunction can be implemented by nand, and nand can, in return, be implemented in transistor. In other words, we can use transistors to implement $c(u,v)$ in base-2.

$r(u,v)$ is a little more tricky:

|u|v|r(u,v)|
|-|-|-|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

There is no single logical operator in C to perform this operation. However, in mathematics, exclusive-or is an exact match. In other words, $r(u,v) = u \oplus v$ in base-2. If insisted, it is also possible to use the "regular" C logical operators to implement $r(u,v)$:

```c
unsigned r(unsigned u, unsigned v)
{
  return ((u && !v) || (!u && v)) ? 1 : 0;
}
```

This is because $u \oplus v = (u \wedge \neg v) \vee (\neg u \wedge v)$. Try to prove this using a truth table as an exercise.

Despite being a little more complex, $r(u,v)$ can also be expressed using logical-negation, conjunction and disjunction. Since all three logical operators can be implemented using nand, and nand can be implemented using transistors, $r(u,v)$ can be implemented using transistors.

This concludes that binary addition can be implemented using transistors!

# Subtraction
