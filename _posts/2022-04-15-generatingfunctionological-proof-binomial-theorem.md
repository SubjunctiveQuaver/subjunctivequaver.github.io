---
title: A generatingfunctionological proof of the binomial theorem
date: 2022-04-16 13:00:00 +1000
categories: [Epic Maths Time, New Perspectives]
tags: [combinatorics, algebra, uni-maths] # TAG names should always be lowercase
math: true
---

Make sure you have read [the last post on generating functions](https://subjunctivequaver.github.io/posts/generatingfunctionological-proof-geometric-arithmetic-sequences/) first, else proceed at your own risk!

Recall that for $$k,n \in \mathbb{N}$$, the **binomial coefficient** is defined by

$$\binom{k}{n} = \frac{k!}{n!(k - n)!} = \frac{\overbrace{k(k - 1)(k - 2)\dotsb(k - n + 1)}^{n\ \text{terms}}}{n!}.$$

You may remember from high school that for some $$k \in \mathbb{N}$$,

$$(x + y)^k = \sum_{n = 0}^k \binom{k}{n} x^n y^{k - n} \implies (1 + x)^k = \sum_{n = 0}^k \binom{k}{n} x^n = \underbrace{\binom{k}{0}}_{= 1} + \underbrace{\binom{k}{1}}_{= k} x + \underbrace{\binom{k}{2}}_{= \frac{k(k - 1)}{2}} x^2 + \dotsb + \underbrace{\binom{k}{k}}_{= 1}x^k.$$

This is the *binomial theorem*.

## The generalised binomial theorem: redefining binomial coefficients

But what if we do not restrict $k$ to be a natural number above? This leads us to [*Newton's generalised binomial theorem*](https://en.wikipedia.org/wiki/Binomial_theorem#Newton's_generalized_binomial_theorem), involving the *binomial series*:

**Theorem 1 (binomial theorem).** If $$\alpha \in \mathbb{R}$$, then

$$(1 + x)^\alpha = \sum_{n \geq 0} \binom{\alpha}{n} x^n \overset{\text{ops}}{\leftrightarrow} \left(\binom{\alpha}{n}\right)_n;$$

this is an equality in the formal sense, where we don't care about convergence. (Note that the series converges when $$\|x\| < 1$$ in the analytic sense.)

What exactly does $$\binom{\alpha}{n}$$ mean for $$\alpha \not\in \mathbb{N}$$? The factorials are no longer well-defined (even if we consider the [Gamma function](https://en.wikipedia.org/wiki/Gamma_function) $$\Gamma$$ where $$\Gamma(n) = (n - 1)!$$ and enforce that $$\alpha! = \Gamma(\alpha + 1)$$, this still fails for negative integers since $$\Gamma$$ is not defined there); so we instead use this definition:

**Definition 1.** The binomial coefficient $$\binom{\alpha}{n}$$, where $$\alpha \in \mathbb{R}$$, is defined by

$$\binom{\alpha}{n} := \frac{\overbrace{\alpha(\alpha - 1)(\alpha - 2)\dotsb(\alpha - n + 1)}^{n\ \text{terms}}}{n!}.$$

In the case that $$\alpha \in \mathbb{N}$$, this obviously agrees with the usual definition, as noted above. Let's prove the binomial theorem using generating functions! The proof turns out to be quite interesting, and involves solving a *differential equation*!

## A generatingfunctionological proof of the binomial theorem

Fix $$\alpha \in \mathbb{R}$$ and let $$A \overset{\text{ops}}{\leftrightarrow} \left(\binom{\alpha}{n}\right)_n$$; this is the generating function of the binomial coefficients. Note that when $$\alpha \in \mathbb{N}$$, these terms eventually become 0, but usually we get infinitely many nonzero terms. Our goal is to show that $$A = (1 + x)^\alpha$$.

Note that

$$\frac{\binom{\alpha}{n}}{\binom{\alpha}{n + 1}} = \frac{\alpha(\alpha - 1)\dotsb(\alpha - n + 1)}{\alpha(\alpha - 1)\dotsb(\alpha - n + 1)(\alpha - n)} \frac{(n + 1)!}{n!} = \frac{n + 1}{\alpha - n} \implies (n + 1)\binom{\alpha}{n + 1} = (\alpha - n)\binom{\alpha}{n};$$

this is a recurrence for the binomial coefficients that holds for $$n \geq 0$$, with $$\binom{\alpha}{0} = \frac{1}{0!} = 1$$, since 1 is the empty product.

Now recall that if $$A \overset{\text{ops}}{\leftrightarrow} (a_n)$$, then $$DA \overset{\text{ops}}{\leftrightarrow} ((n + 1)a_{n + 1})$$; this is precisely the left hand side of our recurrence! In summary, and using [rule 2](https://subjunctivequaver.github.io/posts/generatingfunctionological-proof-geometric-arithmetic-sequences/) (on polynomials), we see

$$\left((n + 1)\binom{\alpha}{n + 1}\right)_n \overset{\text{ops}}{\leftrightarrow} DA \quad \text{and} \quad \left((\alpha - n)\binom{\alpha}{n}\right)_n \overset{\text{ops}}{\leftrightarrow} (\alpha - xD)A.$$

So $$DA = (\alpha - xD)A \implies (1 + x)DA = \alpha A$$. This is a *differential equation* that the generating function for the binomial coefficients satisfy! We can use the theory of differential equations, in particular the integrating factor method (this is a first order linear ODE), to write this as

$$\left(\frac{1}{1 + x}\right)^\alpha DA - \alpha \left(\frac{1}{1 + x}\right)^{\alpha + 1} A = 0$$

and observe that this gives

$$D\left(\left(\frac{1}{1 + x}\right)^\alpha A\right) = 0 \implies \left(\frac{1}{1 + x}\right)^\alpha A = 1$$

where we use the initial condition $$A_0 = \binom{\alpha}{0} = 1$$. Then rearranging, we see that

$$A = \left(\frac{1}{1 + x}\right)^{-\alpha} = (1 + x)^\alpha,$$

and we are done -- we have proved that

$$(1 + x)^\alpha = \sum_{n \geq 0} \binom{\alpha}{n} x^n \overset{\text{ops}}{\leftrightarrow} \left(\binom{\alpha}{n}\right)_n!$$

### Applying the theorem to the Catalan numbers

Recall from the [last post](https://subjunctivequaver.github.io/posts/generatingfunctionological-proof-geometric-arithmetic-sequences/) that **Catalan numbers** count, for instance, the number of ways to have a balanced string of parentheses of length $$2n$$, e.g. something like `(()(()))(())`, but not `())((())`. Then it turns out that $$C_n = \frac{1}{n + 1} \binom{2n}{n}$$, and their generating function is

$$C = \frac{1 - \sqrt{1 - 4x}}{2x}.$$

Let's use the binomial theorem with $$\alpha = 1/2$$, to recover the general formula for $$C_n$$. This is useful, because for instance in the balanced parentheses problem, we can use a combinatorial argument to show that the generating function is $$C$$, but a priori, we don't know an explicit formula for $$C_n$$ (or some similar problem).

First recognise that

$$-C = \frac{\sqrt{1 - 4x} - 1}{2x} = \frac{1}{x}\left(\frac{\sqrt{1 - 4x}}{2} - \frac{1}{2}\right);$$

by the binomial theorem,

$$\sqrt{1 - 4x} = (1 - 4x)^{1/2} = \sum_{n \geq 0} \binom{1/2}{n} (-4x)^n = \sum_{n \geq 0} \binom{1/2}{n} (-4)^n x^n$$

where $$\frac{1}{2}\binom{1/2}{0}(-4)^0 = \frac{1}{2}$$, so we recognise

$$-C \overset{\text{ops}}{\leftrightarrow} \left(\frac{1}{2}\binom{1/2}{n + 1}(-4)^{n + 1}\right) \implies C \overset{\text{ops}}{\leftrightarrow} \left(\binom{1/2}{n + 1}(-1)^n 2^{2n + 1}\right)$$

using [rule 1](https://subjunctivequaver.github.io/posts/generatingfunctionological-proof-geometric-arithmetic-sequences/) (with $$m = 1$$). Then it remains to check

$$\begin{align*}
C_n = [x^n]C &= \binom{1/2}{n + 1}(-1)^n 2^{2n + 1} = \frac{\overbrace{(1/2)(-1/2)(-3/2)\dotsb(-(2n-1)/2)}^{n\ \text{terms}}}{(n + 1)!}(-1)^n 2^{2n + 1} \\
&= \frac{1 \cdot 3 \cdot 5 \dotsb (2n - 1)}{2^{n + 1} \cdot (n + 1)!}2^{2n + 1} = \underbrace{\frac{2 \cdot 4 \cdot 6 \dotsb 2n}{2^n \cdot n!}}_{= 1} \cdot \frac{1 \cdot 3 \cdot 5 \dotsb (2n - 1)}{(n + 1)!} 2^n \\
&= \frac{1}{n + 1} \cdot \frac{(2n)!}{(n!)^2} = \frac{1}{n + 1}\binom{2n}{n},
\end{align*}$$

which is the claimed formula for the Catalan numbers! OK, that's enough for now; see you next year probably with my current rate of writing posts :P
