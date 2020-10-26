[TOC]



# Lecture 1: Asymptotic Algorithm Analysis



## Objective:

- [ ] Understand best, worst, and average cases
- [ ] Understand Big-Oh, Big-Omega, Big-Theta notations
- [ ] Know how to analyze time complexity of a program



## Best, Worst, Average Cases

- **Best case:** 对应ideal input, 所需要的最少的number of steps
- **Worst case:** 对应most difficult input, 所需要的最多的number of steps
- **Average case:** 对应random inputs, 所需要的平均number of steps

*👀注意：*

> 如果说“我的程序在n = 1（single input）的时候是best case因为这是最快的” 这句话是❌的
>
> 因为best case的意思是一个在对于任何size $n$的input时的一个代价最低的<u>special input</u>



### ❓在分析一个算法的时候分析哪种case❓

> 通常用average case / worst case。Average case看起来比较公平，但是需要知道distribution of inputs, 比较难确定。Worst case比较容易分析，而且给了upper bound



### ❓如何分析算法的复杂度❓

#### **I. Ignore constant factors**

1. 比较容易
2. Constants depend on architecture, compiler, etc.
3. Lose very little predictive power

#### II. Focus on running time for large input size $n$

1. Scaling is very important，因为一个算法在input少跟多的时候差别可能会很大

2. We compare the runtime of two algorithm when $n$ is very large.

   > $1000log_2n$ is better than $0.001n$

****



## Asymptotic Analysis: Big-Oh

- **定义：**对于一个值非负的方程 $T(n)$ 来说，如果<u>存在</u>两个正的常数 $c$ 和 $n_0$， 使得$T(n)\le cf(n)$ for all $n > n_0$, 那么方程$T(n)$ 就是在集合 $O(f(n))$里
- **含义：**当数据足够大时$(n\ge n_0)$时，该算法执行的步骤数总<u>小于</u>$cf(n)$ 对于best/ average/ worst case.



### Big-Oh Notation

Big-oh notation indicates an upper bound, 通常我们寻找==tightest upper bound==

#### 👀 I. A sufficient condition of Big-Oh

<img src="/Users/michaelxu/Library/Application Support/typora-user-images/image-20200911194051559.png" alt="image-20200911194051559" style="zoom:50%;" />



#### II. Rules of Big-Oh

<img src="/Users/michaelxu/Library/Application Support/typora-user-images/image-20200926193345039.png" alt="image-20200926193345039" style="zoom:50%;" />

<img src="/Users/michaelxu/Library/Application Support/typora-user-images/image-20200926193404044.png" alt="image-20200926193404044" style="zoom:50%;" />



#### III. A Few Results about Common Functions

<img src="/Users/michaelxu/Library/Application Support/typora-user-images/image-20200926193518935.png" alt="image-20200926193518935" style="zoom:50%;" />

👀**练习：**

<img src="/Users/michaelxu/Library/Application Support/typora-user-images/image-20200926193650699.png" alt="image-20200926193650699" style="zoom:50%;" />

****



## Relative of Big-Oh: 1. Big-Omega

- **定义：** 对于一个值非负的方程 $T(n)$ 来说，如果<u>存在</u>两个正的常数 $c$ 和 $n_0$， 使得$T(n)\ge cg(n)$ for all $n > n_0$, 那么方程$T(n)$ 就是在集合 $\Omega (g(n))$里
- **含义：**对于所有足够大的数据（$n > n_0$), 该算法始终需要比$cg(n)$更多的步骤

⚠️ Big-Omega gives a lower bound, we usually want ==the greatest lower bound==

> ❓What is the big-omega notation for $T(n) = c_1(n^2) + c_2(n)$❓
>
> Answer：$T(n) = O(n^2) = \Omega (n^2)$



# Relative of Big-Oh: 2. Big-Theta

- **定义：**如果$T(n)$在集合$O(g(n))$以及$\Omega(g(n))$中, 那么称$T(n)$在集合$\theta(g(n))$中。
  - 数学含义：存在三个正的常数，$c1, c2, n0$ 使得对于所有的$n > n_0$ ,都有$c_1g(n) \le T(n) \le c_2g(n)$

🌰

<img src="/Users/michaelxu/Library/Application Support/typora-user-images/image-20201026191344150.png" alt="image-20201026191344150" style="zoom:40%;" />

