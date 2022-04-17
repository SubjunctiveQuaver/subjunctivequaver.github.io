---
title: A generatingfunctionological proof of the geometric and arithmetic sequence formulas
date: 2022-04-16 11:28:00 +1000
categories: [Epic Maths Time, New Perspectives]
tags: [combinatorics, algebra, uni-maths] # TAG names should always be lowercase
math: true
---

Recall from high school that a **geometric sequence** is a sequence $$(a_n)_{n \geq 0}$$ that satisfies the *recurrence relation* $$a_{n + 1} = r a_n$$ for some fixed $$r \in \mathbb{R}$$, and an **arithmetic sequence** is a sequence $$(b_n)_{n \geq 0}$$ that satisfies $$b_{n + 1} = b_n + d$$ for some fixed $$d \in \mathbb{R}$$.

For example, the sequences $$(1,2,4,8,16,\dotsc)$$ and $$(1,-1,1,-1,1,\dotsc)$$ are geometric, while the sequences $$(0,1,2,3,4,\dotsc)$$ and $$(11,7,3,-1,-5,\dotsc)$$ are arithmetic.

You may recall, again from high school, the formulas

$$a_n = a_0 r^n \quad \text{and} \quad b_n = b_0 + nd$$

for a generic term of the above geometric and arithmetic sequences, respectively.

**Exercise 1.** Verify that the above two formulas for geometric and arithmetic sequences hold, using a proof by induction or similar approach.

In this post, I will introduce a totally overkill approach of deriving these two formulas; this approach will turn out to be a general approach to solving many recurrence relations. The key to this approach is to use *generating functions*.

## A "naive" approach for geometric sequences

Starting with $$a_{n + 1} = ra_n$$, multiply by $$x^n$$ and sum over all $$n \geq 0$$ (for which this recurrence is valid for) to get

$$\sum_{n \geq 0} a_{n + 1}x^n = \sum_{n \geq 0} ra_n x^n = r \sum_{n \geq 0} a_n x^n.$$

If we let $$A(x) = \sum_{n \geq 0} a_n x^n$$, then surely

$$\sum_{n \geq 0} a_{n + 1}x^n = \sum_{n \geq 1} a_nx^{n - 1} = \frac{1}{x} \sum_{n \geq 1} a_nx^n = \frac{1}{x} \left(\sum_{n \geq 0} a_nx^n - a_0\right) = \frac{1}{x}(A(x) - a_0),$$

so we get the equation

$$\frac{1}{x}(A(x) - a_0) = rA(x) \implies A(x) = \frac{a_0}{1 - rx} = a_0 \sum_{n \geq 0} (rx)^n = \sum_{n \geq 0} a_0 r^n x^n.$$

But recall that $$A(x) = \sum_{n \geq 0} a_n x^n$$, so we must surely have $$a_n = a_0 r^n$$, which agrees with the known formula!

So we solved the recurrence relation by using some sort of magical overkill power series approach. How exactly does it work, can we be more methodical, and is it even useful? I will attempt to answer that in the rest of this post.

## Generating functions

Unless otherwise stated, all sequences $$(a_n)_{n \geq 0} = (a_0,a_1,\dotsc)$$ start with a zeroth term $$a_0$$; I simply write $$(a_n)$$.

**Definition 1.** Consider a sequence $$(a_n)$$. The **(ordinary) generating function** of $$(a_n)$$ is the *(formal) power series*

$$A = \sum_{n \geq 0}a_n x^n = a_0 + a_1x + a_2x^2 + \dotsb$$

where the coefficient of $$x^n$$, denoted $$[x^n]A$$, is precisely $$a_n$$. We write $$(a_n) \overset{\text{ops}}{\leftrightarrow} A$$.

These power series are *formal* in the sense that we do not care about convergence: they are not analytic. In general, the $$x$$ is to be interpreted as an indeterminate; a symbol that can be manipulated, but does not have meaning on its own. Representing a sequence in this way serves as to ensure that the terms in the sequence remain "separated" -- they are separated by powers of $$x$$.

### The ring of formal power series

Every formal power series is associated with a unique sequence -- its sequence of coefficients -- and vice versa. Two formal power series are equal if and only if the sequences of coefficients are equal.

The set of formal power series forms a **ring** $$\mathbb{R}[[x]]$$ in a natural way (where the coefficients are in $$\mathbb{R}$$); the addition is given by

$$\left(\sum_{n \geq 0}a_n x^n\right) + \left(\sum_{n \geq 0}b_n x^n\right) = \sum_{n \geq 0} (a_n + b_n)x^n,$$

and the (commutative) multiplication is given by

$$\left(\sum_{n \geq 0}a_n x^n\right)\left(\sum_{n \geq 0}b_n x^n\right) = \sum_{n \geq 0} \left(\sum_{k = 0}^n a_k b_{n - k}\right)x^n;$$

this looks funny but it's what we would expect when we try to multiply out an (infinite) expression of the form

$$(a_0 + a_1x + a_2x^2 + \dotsb)(b_0 + b_1x + b_2x^2 + \dotsb) = a_0b_0 + (a_0b_1 + a_1b_0)x + (a_0b_2 + a_1b_1 + a_2b_0)x^2 + \dotsb$$

which it precisely is. The additive identity (zero) in $$\mathbb{R}[[x]]$$ is the power series $$0 = 0 + 0x + 0x^2 + \dotsb \overset{\text{ops}}{\leftrightarrow} (0)$$. The multiplicative identity (unit) in $$\mathbb{R}[[x]]$$ is the power series $$1 = 1 + 0x + 0x^2 + \dotsb \overset{\text{ops}}{\leftrightarrow} (1,0,0,\dotsc)$$.

For example, the (multiplicative) inverse of the power series $$1 - x = 1 - x + 0x^2 + 0x^3 + \dotsb$$ turns out to be $$\sum_{n \geq 0}x^n = 1 + x + x^2 + \dotsb$$; we can verify this by computing

$$(1 - x)(1 + x + x^2 + \dotsb) = 1 + (1 - 1)x + (1 - 1 + 0)x^2 + \dotsb = 1.$$

So it is reasonable to write that

$$\frac{1}{1 - x} = \sum_{n \geq 0} x^n = 1 + x + x^2 + \dotsb;$$

this is true in the formal sense, not just for $$\lvert x\rvert < 1$$ as in the analytical case. However, when the power series in the analytical sense converges, it is reasonable to substitute in numerical values for $$x$$. This also gives us our first (simple) result:

**Lemma 1.** Let $$(1) = (1,1,\dotsc)$$ be the constant sequence; then

$$\frac{1}{1 - x} \overset{\text{ops}}{\leftrightarrow} (1).$$

Note that extracting coefficients from power series is somehow "linear", in the sense that $$[x^n](A + kB) = [x^n]A + k[x^n]B$$ (the formal power series also form a *vector space* over $$\mathbb{R}$$, and this is a linear map (functional) $$\mathbb{R}[[x]] \to \mathbb{R}$$). This is a useful fact that we use later.

![Extracting coefficients from formal power series is linear: a useful tool that will help us later.](https://i.imgflip.com/31po1l.png)

## Solving recurrences -- a generatingfunctionological approach

Throughout this section, let $$(a_n) \overset{\text{ops}}{\leftrightarrow} A$$. A **generatingfunctionological** approach, as coined in [Wilf's book "generatingfunctionology"](https://www2.math.upenn.edu/~wilf/DownldGF.html), is an approach to working with sequences using their generating functions.

**Definition 2.** Let $$(a_n)$$ be a sequence. Then a ($$k$$th order) **recurrence** for $$(a_n)$$ is an equation $$\varphi(n,a_n,a_{n + 1},\dotsc,a_{n + k}) = 0$$ which holds for particular $$n$$.

If we fix a value of $$n$$, then a recurrence gives us one equation that $$(a_n)$$ satisfies. However, the expression

$$\sum_n \varphi(n,a_n,a_{n + 1},\dotsc,a_{n + k})x^n = 0$$

simultaneously encodes *every* equation that $$(a_n)$$ satisfies that is given by the recurrence. In the (usual) case that $$n$$ ranges over $$\mathbb{N}$$, we recover the generating function of $$(a_n)$$; otherwise observe for instance that $$\sum_{n \geq N} a_n x^n = A - a_0 - a_1x - \dotsb - a_{N - 1}x^{N - 1}$$.

Thus, to solve a recurrence relation, we can attempt to convert the recurrence for $$(a_n)$$ into an equation involving its generating function $$A$$ by finding the generating functions of the sequences equated in the recurrence; then if we can solve this for $$A$$, then we have found $$a_n = [x^n]A$$. However, we may not explicitly find $$A$$ as a (formal) power series; using different techniques (such as partial fractions or the binomial theorem) we can find a power series expansion to extract the coefficients $$a_n$$.

A recurrence is **linear** if $$a_{n + k} = f_0 a_n + f_1 a_{n + 1} + \dotsb + f_{k - 1} a_{n + k - 1}$$ for some $$k$$, where each $$f_i$$, a **coefficient**, is a function of $$n$$. We present a quick theorem without proof:

**Theorem 1.** Let $$A \overset{\text{ops}}{\leftrightarrow} (a_n)$$. Then $$A$$ is a rational function $$p/q$$ (where $$p,q$$ have lowest possible degree) with $$\deg q = k$$ if and only if $$(a_n)$$ satisfies a linear recurrence with constant coefficients of order $$k$$.

After reading this article, you will have the tools to prove this theorem yourself! (If you want to, of course!) One direction is by the technique for finding a generating function outlined below, and the other direction follows by considering an expansion of $$q A = p$$.

### The algebra and calculus of generating functions

**Definition 3.** The **(formal) derivative** of a power series $$A = \sum_{n \geq 0} a_nx^n \overset{\text{ops}}{\leftrightarrow} (a_n)$$ is the power series

$$DA = \sum_{n \geq 1} n a_n x^{n - 1} = \sum_{n \geq 0} (n + 1)a_{n + 1}x^n \overset{\text{ops}}{\leftrightarrow} ((n + 1)a_{n + 1}).$$

The **derivative operator** $$D$$ on $$\mathbb{R}[[x]]$$ is the map $$A \mapsto DA$$.

We can verify some expected properties of the derivative operator: it is a **derivation** on $$\mathbb{R}[[x]]$$ (let $$A,B \in \mathbb{R}[[x]]$$), since

- It is *linear* (where we think of $$\mathbb{R}[[x]]$$ as a vector space): $$D(A + kB) = DA + kDB$$ where $$k \in \mathbb{R}$$,
- It satisfies a sort of *(Leibniz) product rule*: $$D(AB) = A(DB) + (DA)B$$.

**Exercise 2.** Check thse both! Remember to use the correct rule for multiplying power series for the product rule.

We can also combine the derivative operator with other operators on $$\mathbb{R}[[x]]$$. For operators $$S,T$$, define their **sum** $$S + T$$ to be the map $$A \mapsto SA + TA$$ (*pointwise addtion*), and their **product** $$ST$$ to be the map $$A \mapsto S(TA)$$ (*composition of operators*). The $$k$$th **iterate** of $$T$$ is defined by $$T^k := \underbrace{TT\dotsb T}_{k\ \text{copies}}$$, which is the map $$A \mapsto \underbrace{T(T(\dotsb(TA)\dotsb))}_{k\ \text{times}}$$.

*Repeated differentiation* is denoted by $$D^k$$, i.e. $$D^kA$$ is the $$k$$th (formal) derivative of $$A$$. Another common operator that comes up when solving recurrences is the **~~ecks dee~~ xD operator** $$xD$$ on $$\mathbb{R}[[x]]$$, defined as the map $$A \mapsto xDA$$, i.e. differentiation then multiplication by $$x$$. We often deal with *polynomials* in $$xD$$, where $$1$$ denotes the **identity operator** $$A \mapsto A$$, but note that $$(xD)^2 = xD(xD) \neq x^2 D^2$$. Indeed,

$$(xD)^2 = xD(xD) = x(D + xD^2) = xD + x^2D^2 \implies (xD)^2A = xDA + x^2D^2A$$

by the product rule. Furthermore, care must be taken as these operators do not generally commute: while $$xD(xD + 1) = (xD)^2 + xD = (xD + 1)xD$$, note that $$Dx \neq xD$$ (we can think of $x$ as an operator on $$\mathbb{R}[[x]]$$ with $$A \mapsto xA$$; then $$Dx1 = Dx = 1 \neq 0 = xD1$$). This is all related to the notion of a [Weyl algebra](https://en.wikipedia.org/wiki/Weyl_algebra), which is a ring of *differential operators* with polynomial coefficients (the addition is pointwise addition, and the product is composition of operators).

**Exercise 3.** Similar to the above, what is an expansion of $$(xD)^k$$ without any powers of $$xD$$? ~~(I haven't tried this yet, but it looks promising.)~~ Update (thanks [Ally](https://piecewise.org/exploration/an-adventure-in-rewriting-polynomials) and Jacob): it looks like

$$(xD)^k = \left\{k \atop 0\right\} + \left\{k \atop 1\right\} xD + \left\{k \atop 2\right\} x^2D^2 + \dotsb + \left\{k \atop k\right\} x^k D^k,$$

where

$$\left\{k \atop n\right\} = \frac{1}{n!} \sum_{i = 0}^n (-1)^i \binom{n}{i} (n - i)^k$$

are [Stirling numbers of the 2nd kind](https://en.wikipedia.org/wiki/Stirling_numbers_of_the_second_kind), which count the number of ways to partition $$[n] = \{1,\dotsc,n\}$$ into $$k$$ (nonempty) parts. (Note that $$\left\{k \atop 0\right\} = 0$$ if $$k \geq 1$$, but $$\left\{0 \atop 0\right\} = 1$$, and $$(xD)^0 = 1 = \operatorname{Id}_{\mathbb{R}[[x]]}$$, so the pattern holds.) Prove/disprove this claim, and post your solutions in the unofficial [Maths @ Monash Discord](https://discord.gg/hx63ZwSXBg)!

Using these, we can identify some rules for the generating functions of some transformations of sequences:

**Lemma 2.** Let $$(a_n) \overset{\text{ops}}{\leftrightarrow} A$$ and $$(b_n) \overset{\text{ops}}{\leftrightarrow} B$$. Then

1. For any fixed $$m > 0$$, $$(a_{n + m}) \overset{\text{ops}}{\leftrightarrow} \frac{1}{x^m}(A - a_0 - a_1x - \dotsb - a_{m - 1}x^{m - 1})$$
2. If $$p(n)$$ is any polynomial in $$n$$, then $$p(xD)A \overset{\text{ops}}{\leftrightarrow} (p(n)a_n)$$
3. $$AB \overset{\text{ops}}{\leftrightarrow} \left(\sum_{k = 0}^n a_k b_{n - k}\right)_n$$
4. For any $$k \in \mathbb{R}$$, $$A + kB \overset{\text{ops}}{\leftrightarrow} (a_n + kb_n)$$
5. $$\frac{A}{1 - x} \overset{\text{ops}}{\leftrightarrow} \left(\sum_{k = 0}^n a_k\right)_n$$
6. For a fixed $$k > 0$$, if $$b_{kn} = a_n$$ for $$n \geq 0$$ and $$b_m = 0$$ otherwise, then $$A(x^k) = B(x) \overset{\text{ops}}{\leftrightarrow} (b_n)$$

Note that in rule 1, we don't mean division by $$x^m$$ in the ring $$\mathbb{R}[[x]]$$, as it does not have an inverse. Rather, it is the [quotient in an Euclidean division](https://math.stackexchange.com/questions/3744068/what-is-the-meaning-of-division-of-a-formal-power-series-by-x) (note that $$\mathbb{R}[[x]]$$ is a *Euclidean domain*).

We give a proof of rule 2; it suffices to prove it for monic monomials; then apply rule 4. Let $$p(n) = n^k$$; then $$p(xD)A = (xD)^kA$$. The case $$k = 0$$ is trivial. Then if $$k > 0$$, we proceed by induction on $$k$$ and note that

$$p(xD)A = (xD)^kA = xD(xD)^{k - 1}A = xD \sum_{n \geq 0} n^{k - 1}a_n x^n = x \sum_{n \geq 1} n^ka_n x^{n - 1} = \sum_{n \geq 0} n^ka_n x^n \overset{\text{ops}}{\leftrightarrow} (n^ka_n) = (p(n)a_n);$$

the 3rd equality is by the inductive hypothesis (i.e. that $$(xD)^{k - 1}A = \sum_{n \geq 0} n^{k - 1}a_n x^n \overset{\text{ops}}{\leftrightarrow} (n^{k - 1}a_n)$$). Thus we are done!

**Exercise 4.** Prove the unproven generating function rules 1,3,4,5,6 above. (Hint for rule 5: use rule 3 and Lemma 1.) Post your solutions in the unofficial [Maths @ Monash Discord](https://discord.gg/hx63ZwSXBg)!

### Finding formulas for the geometric and arithmetic sequences

Using the algebra and calculus of generating functions, we give a succinct generatingfunctionological proof of the formulas for the geometric and arithmetic sequences.

Recall that the **geometric sequence** $$(a_n)_{n \geq 0}$$ satisfies $$a_{n + 1} = r a_n$$. Let $$(a_n) \overset{\text{ops}}{\leftrightarrow} A$$. Then by rule 1, $$(a_{n + 1}) \overset{\text{ops}}{\leftrightarrow} \frac{1}{x}(A - a_0)$$, so the recurrence (and rule 4) yields

$$\frac{1}{x}(A - a_0) = rA \implies A = \frac{a_0}{1 - rx}.$$

Extracting coefficients and using (the surprise tool) linearity, we recover

$$a_n = [x^n]A = a_0[x^n]\sum_{n \geq 0}(rx)^n = a_0r^n.$$

Now, the **arithmetic sequence** $$(b_n)_{n \geq 0}$$ satisfies $$b_{n + 1} = b_n + d$$. Let $$(b_n) \overset{\text{ops}}{\leftrightarrow} B$$. Then by rule 1, $$(b_{n + 1}) \overset{\text{ops}}{\leftrightarrow} \frac{1}{x}(B - b_0)$$; Lemma 1 and rule 4 yields $$(d) \overset{\text{ops}}{\leftrightarrow} \frac{d}{1 - x}$$, so the recurrence (and rule 4) yields (by partial fractions)

$$\frac{1}{x}(B - b_0) = B + \frac{d}{1 - x} \implies B = \frac{b_0 - d}{1 - x} + \frac{d}{(1 - x)^2}.$$

By rule 2 with $$p(n) = n$$, we have

$$xD\frac{1}{1 - x} \overset{\text{ops}}{\leftrightarrow} (p(n)1) = (n) \implies \frac{1}{(1 - x)^2} = \frac{1}{x} \left(xD\frac{1}{1 - x} - 0\right) \overset{\text{ops}}{\leftrightarrow} (n + 1)$$

by rule 1. (There are other ways to do this, such as direct manipulation of the power series, but that's boring!) Thus by linearity, we extract the coefficient

$$b_n = [x^n]B = (b_0 - d)[x^n]\frac{1}{1 - x} + d[x^n]\frac{1}{(1 - x)^2} = (b_0 - d)1 + d(n + 1) = b_0 + dn$$

since $$(1) \overset{\text{ops}}{\leftrightarrow} \frac{1}{1 - x}$$ and $$(n + 1) \overset{\text{ops}}{\leftrightarrow} \frac{1}{(1 - x)^2}$$ (recall what this means). This is the formula for the arithmetic sequence; how awesome! (OK that was totally overkill LOL.)

**Exercise 5.** Show that

$$\frac{1}{(1 - x)^2} \overset{\text{ops}}{\leftrightarrow} (n + 1)$$

in the following alternative ways:

1. Use the fact that $$\frac{1}{(1 - x)^2} = D\frac{1}{1 - x}$$, and explicitly differentiating the power series $$\sum_{n \geq 0} x^n$$ and identifying the coefficient that appears.
2. Use the fact that $$\frac{1}{(1 - x)^2} = D\frac{1}{1 - x}$$ again, but look at the comment in Definition 3 (i.e. that $$DA \overset{\text{ops}}{\leftrightarrow} ((n + 1)a_{n + 1}).$$ if $$A \overset{\text{ops}}{\leftrightarrow} (a_n)$$; choose $$(a_n)$$ carefully).
3. Use fact 5 repeatedly, starting from $A = 1$. (What sequence is this the generating function of?)

Post your solutions in the unofficial [Maths @ Monash Discord](https://discord.gg/hx63ZwSXBg)!

### A few more applications (an outline only)

There are many nice applications of this generatingfunctionological technique. Here are just a few:

- The **Fibonacci sequence** $$(F_n)$$ satisfies the linear recurrence $$F_{n + 2} = F_{n + 1} + F_n$$ for $$n \geq 0$$ with $$F_0 = 0$$ and $$F_1 = 1$$. It has generating function $$F = \frac{x}{1 - x - x^2}$$; we can recover a formula for $$F_n$$ using partial fractions.
- The **binomial theorem** $$(1 + x)^\alpha = \sum_{n \geq 0} \binom{\alpha}{n} x^n \overset{\text{ops}}{\leftrightarrow} \left(\binom{\alpha}{n}\right)_n$$ where $$\alpha \in \mathbb{R}$$. I talk about this in more detail in [the next post](https://subjunctivequaver.github.io/posts/generatingfunctionological-proof-binomial-theorem/)!
- The **Catalan numbers** $$C_n = \frac{1}{n + 1} \binom{2n}{n}$$ have generating function $$C = \frac{1 - \sqrt{1 - 4x}}{2x}$$; using the binomial theorem with $$\alpha = 1/2$$, we can recover this formula for $$C_n$$. Moreover, they satisfy the recurrence $$C_{n + 1} = \sum_{i = 0}^n C_i C_{n - i}$$ with $$C_0 = 1$$; note that $$\left(\sum_{i = 0}^n C_i C_{n - i}\right) \overset{\text{ops}}{\leftrightarrow} C^2$$ by rule 3, so $$\frac{1}{x}(C - 1) = \frac{1}{x}(C - C_0) = C^2 \iff C - 1 = xC^2$$, which can be used to find $$C$$ as before (use the initial condition $$C_0 = 1$$ to pick the negative square root). Note that $$C_n$$ is, for instance, the number of ways to have a balanced string of parentheses of length $$2n$$, e.g. something like `(()(()))(())`, but not `())((())`.

**Exercise 6.** (Adapted from discussion on the [Maths @ Monash Discord](https://discord.gg/hx63ZwSXBg) server.) Consider the **triangular numbers** $$T_n = \frac{n(n + 1)}{2}$$, and define a recurrence $$a_{n + 1} = a_n + T_n$$, with $$a_0 = 0$$. Find a linear recurrence with constant coefficients that $$(a_n)$$ satisfies (consider Theorem 1 above), and use a generatingfunctionological approach to find an explicit formula for $$a_n$$ (feel free to use a computer to find a series expansion). Post your solutions in the unofficial [Maths @ Monash Discord](https://discord.gg/hx63ZwSXBg)!

Happy generatingfunctionologing (and happy Easter too $xD$)!
