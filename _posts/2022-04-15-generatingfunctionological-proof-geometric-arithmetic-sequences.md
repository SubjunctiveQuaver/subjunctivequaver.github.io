---
title: A generatingfunctionological proof of the geometric and arithmetic sequence formulas
date: 2022-04-15 21:23:00 +1000
categories: [Epic Maths Time, New Perspectives]
tags: [combinatorics, algebra, uni-maths] # TAG names should always be lowercase
math: true
---

Recall from high school that a **geometric sequence** is a sequence $(a\_n)\_{n \geq 0}$ that satisfies the *recurrence relation* $a\_{n + 1} = r a\_n$ for some fixed $r \in \mathbb{R}$, and an **arithmetic sequence** is a sequence $(b\_n)\_{n \geq 0}$ that satisfies $b_{n + 1} = b_n + d$ for some fixed $d \in \mathbb{R}$.

For example, the sequences $(1,2,4,8,16,\dotsc)$ and $(1,-1,1,-1,1,\dotsc)$ are geometric, while the sequences $(0,1,2,3,4,\dotsc)$ and $(11,7,3,-1,-5,\dotsc)$ are arithmetic.

You may recall, again from high school, the formulas

$$a_n = a_0 r^n \quad \text{and} \quad b_n = a_0 + nd$$

for a generic term of the above geometric and arithmetic sequences, respectively.

**Exercise 1.** Verify that the above two formulas for geometric and arithmetic sequences hold, using a proof by induction or similar approach.

In this post, I will introduce a totally overkill approach of deriving these two formulas; this approach will turn out to be a general approach to solving many recurrence relations. The key to this approach is to use *generating functions*.

## A "naive" approach for geometric sequences

Starting with $a_{n + 1} = ra_n$, multiply by $x^n$ and sum over all $n \geq 0$ (for which this recurrence is valid for) to get

$$\sum_{n \geq 0} a_{n + 1}x^n = \sum_{n \geq 0} ra_n x^n = r \sum_{n \geq 0} a_n x^n.$$

If we let $A(x) = \sum_{n \geq 0} a_n x^n$, then surely

$$\sum_{n \geq 0} a_{n + 1}x^n = \sum_{n \geq 1} a_nx^{n - 1} = \frac{1}{x} \sum_{n \geq 1} a_nx^n = \frac{1}{x} \left(\sum_{n \geq 0} a_nx^n - a_0\right) = \frac{1}{x}(A(x) - a_0),$$

so we get the equation

$$\frac{1}{x}(A(x) - a_0) = rA(x) \implies A(x) = \frac{a_0}{1 - rx} = a_0 \sum_{n \geq 0} (rx)^n = \sum_{n \geq 0} a_0 r^n x^n.$$

But recall that $A(x) = \sum_{n \geq 0} a_n x^n$, so we must surely have $a_n = a_0 r^n$, which agrees with the known formula!

So we solved the recurrence relation by using some sort of magical overkill power series approach. How exactly does it work, can we be more methodical, and is it even useful? I will attempt to answer that in the rest of this post.

## Generating functions

Unless otherwise stated, all sequences $(a_n)_{n \geq 0} = (a_0,a_1,\dotsc)$ start with a zeroth term $a_0$; I simply write $(a_n)$.

**Definition 1.** Consider a sequence $(a_n)$. The **(ordinary) generating function** of $(a_n)$ is the *(formal) power series*

$$A = \sum_{n \geq 0}a_n x^n = a_0 + a_1x + a_2x^2 + \dotsb$$

where the coefficient of $x^n$, denoted $[x^n]A$, is precisely $a_n$. We write $(a_n) \overset{\text{ops}}{\leftrightarrow} A$.

These power series are *formal* in the sense that we do not care about convergence: they are not analytic. In general, the $x$ is to be interpreted as an indeterminate; a symbol that can be manipulated, but does not have meaning on its own. Representing a sequence in this way serves as to ensure that the terms in the sequence remain "separated" -- they separated by powers of $x$.

### The ring of formal power series

Every formal power series is associated with a unique sequence -- its sequence of coefficients -- and vice versa. Two formal power series are equal if and only if the sequences of coefficients are equal.

The set of formal power series forms a **ring** $\mathbb{R}[[x]]$ in a natural way (where the coefficients are in $\mathbb{R}$); the addition is given by

$$\left(\sum_{n \geq 0}a_n x^n\right) + \left(\sum_{n \geq 0}b_n x^n\right) = \sum_{n \geq 0} (a_n + b_n)x^n,$$

and the (commutative) multiplication is given by

$$\left(\sum_{n \geq 0}a_n x^n\right)\left(\sum_{n \geq 0}b_n x^n\right) = \sum_{n \geq 0} \left(\sum_{k = 0}^n a_k b_{n - k}\right)x^n;$$

this looks funny but it's what we would expect when we try to multiply out an (infinite) expression of the form

$$(a_0 + a_1x + a_2x^2 + \dotsb)(b_0 + b_1x + b_2x^2 + \dotsb) = a_0b_0 + (a_0b_1 + a_1b_0)x + (a_0b_2 + a_1b_1 + a_2b_0)x^2 + \dotsb$$

which it precisely is. The multiplicative identity in $\mathbb{R}[[x]]$ is the power series $1 = 1 + 0x + 0x^2 + \dotsb$.

For example, the (multiplicative) inverse of the power series $1 - x = 1 - x + 0x^2 + 0x^3 + \dotsb$ turns out to be $\sum_{n \geq 0}x^n = 1 + x + x^2 + \dotsb$; we can verify this by computing

$$(1 - x)(1 + x + x^2 + \dotsb) = 1 + (1 - 1)x + (1 - 1 + 0)x^2 + \dotsb = 1.$$

So it is reasonable to write that

$$\frac{1}{1 - x} = \sum_{n \geq 0} x^n = 1 + x + x^2 + \dotsb;$$

this is true in the formal sense, not just for $\|x\| < 1$ as in the analytical case. However, when the power series in the analytical sense converges, it is reasonable to substitute in numerical values for $x$. This also gives us our first (simple) result:

**Lemma 1.** Let $(1) = (1,1,\dotsc)$ be the constant sequence; then

$$\frac{1}{1 - x} \overset{\text{ops}}{\leftrightarrow} (1).$$

## Solving recurrences -- a generatingfunctionological approach

Throughout this section, let $(a_n) \overset{\text{ops}}{\leftrightarrow} A$.

**Definition 2.** Let $(a_n)$ be a sequence. Then a **recurrence** for $(a_n)$ is an equation $f(a_n,a_{n + 1},a_{n + 2},\dotsc) = 0$ which holds for $n \geq k$ for some $k$.

If we fix a value of $n$, then a recurrence gives us one equation that $(a_n)$ satisfies. However, the expression

$$f\left(\sum_{n \geq k}a_n x^n,\sum_{n \geq k}a_{n + 1} x^n,\sum_{n \geq k}a_{n + 2} x^n,\dotsc\right) = 0$$

simultaneously encodes *every* equation that $(a_n)$ satisfies that is given by the recurrence. In the (usual) case that $k = 0$, we recover the generating function of $(a_n)$; otherwise observe that $\sum_{n \geq k}a_n x^n = A - a_0 - a_1x - \dotsb - a_{k - 1}x^{k - 1}$.

Thus, to solve a recurrence relation, we can attempt to convert the recurrence for $(a_n)$ into an equation involving its generating function $A$; then if we can solve this for $A$, then we have found $a_n = [x^n]A$. However, we may not explicitly find $A$ as a (formal) power series; using different techniques (such as partial fractions or the binomial theorem) we can find a power series expansion to extract the $a_n$.

### The algebra and calculus of generating functions

- Formal derivative of power series
- The $xD$ operator
- Rules for generating functions

### Finding formulas for the geometric and arithmetic sequences

### A few more applications (an outline only)

- Fibonacci sequence
- Catalan numbers
