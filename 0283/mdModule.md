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

Based on these functions, we can now relate the digits based on their rows and columns. $q_i = r(x_i,y_i)$, $s_i = r(q_i, k_i)$, and $k_{i+1}=c(x_i,y_i)+c(q_i,k_i)$

# Subtraction
