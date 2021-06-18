---
title: Why probability and statistics need measure theory, part 2
date: 2021-06-18 13:14:00 +1000
categories: [Epic Maths Time, New Perspectives]
tags: [probability, measure-theory, statistics, topology, uni-maths]     # TAG names should always be lowercase
math: true
---

If you haven't already read part 1, make sure you read it [here](https://subjunctivequaver.github.io/posts/measure-theory-in-probability/) first! Or else, much of the below will not make sense!

## Random variables: neither random, nor a variable

### What is a random variable?

Let $$(\Omega,\mathcal F,\mathbb P)$$ be a probability space.

**Definition 10.** A **random variable** is a *measurable* function $$X : \Omega \to E$$, where $$(E,\mathcal E)$$ is the **state space**. We usually take $$E$$ to be a topological space $$(E,\mathcal T)$$ (e.g. $$\mathbb R,\mathbb R^n,\mathbb C$$ with the usual topologies), so that $$(E,\mathcal B)$$ is endowed with the *Borel sigma algebra*.

Clearly we must define measurable functions.

**Definition 11.** A function $$f : (\Omega,\mathcal F) \to (E,\mathcal E)$$ between measurable spaces is **measurable** if, for any measurable subset $$A \in \mathcal E$$ of $$E$$, its *preimage*

$$f^{-1}(A) := \{x \in \Omega : f(x) \in A\}$$

is measurable in $$\Omega$$, i.e. $$f^{-1}(A) \in \mathcal F$$. If $$(E,\mathcal T)$$ is a topological space and $$\mathcal E = \mathcal B(\mathcal T)$$, then $$f$$ is **Borel measurable**.

For now, we will take $$\Omega = E = \mathbb R$$, and the Borel sigma algebra on $$\mathbb R$$. What are some examples of measurable functions? Well, it turns out that every function you can think of (well, with probability 1) will be measurable! One particularly nice class of measurable functions in this case are the *continuous functions*:

**Definition 12.** A function $$f : (\Omega,\tau) \to (E,\mathcal T)$$ between *topological spaces* is **continuous** if, for any open subset $$A \in \mathcal T$$ of $$E$$, its *preimage* $$f^{-1}(A)$$ is open in $$\Omega$$, i.e. $$f^{-1}(A) \in \tau$$.

Hopefully you can see the similarity: just replace "measurable" with "open"! Again, this may be different to the usual notion of continuity that you know (nearby inputs map to nearby outputs), but they turn out to be [equivalent](https://math.stackexchange.com/questions/2762135/equivalence-of-continuity-between-metric-and-topological-spaces). Here is a quick proof of the above claim:

**Proposition 13.** Suppose $$f : (\Omega,\tau) \to (E,\mathcal T)$$ is a *continuous* function. Then for a sigma algebra $$\mathcal F$$ on $$\Omega$$ that *contains* the Borel sigma algebra $$\mathcal B(\tau)$$, the function $$f : (\Omega,\mathcal F) \to (E,\mathcal B(\mathcal T))$$ is *measurable*.

*Proof.* Let $$A \in \mathcal B(\mathcal T)$$ be a Borel set. Recall that this means that there is a countable sequence of union/intersection/complement operations such that $$A$$ is constructed from a (countable) family of open sets $$(A_i)_{i \in I}$$. But note that the preimage of any union/intersection/complement is the union/intersection/complement of the preimages (in general, $$f^{-1}(A \cup B) = f^{-1}(A) \cup f^{-1}(B)$$, $$f^{-1}(A \cap B) = f^{-1}(A) \cap f^{-1}(B)$$, and $$f^{-1}(A \setminus B) = f^{-1}(A) \setminus f^{-1}(B)$$), so it follows that $$f^{-1}(A)$$ is constructed from the sets $$(f^{-1}(A_i))_{i \in I}$$ using the exact same sequence of operations. But $$f^{-1}(A_i)$$ is open for any $$i$$ by continuity of $$f$$ (by definition), thus measurable (since $$\mathcal F$$ contains $$\mathcal B(\tau)$$, which contains all open sets in $$\Omega$$). So $$f^{-1}(A)$$ is constructed from the measurable sets $$(f^{-1}(A_i))_{i \in I}$$ using a countable sequence of union/intersection/complement operations, so $$f^{-1}(A) \in \mathcal F$$ (sigma algebras are closed under these operations). $$\square$$

This immediately gives many, many measurable functions! Assuming the sample space is $$\mathbb R$$, polynomial functions, rational functions, exponentials, trigonometric functions, logarithmic functions etc. are all measurable, and so are their sums, products, quotients (where defined), and compositions (which are all continuous)! So are the minimum/maximum of two continuous/measurable functions (in fact, supremums and infimums also work). So is the wild [Weierstrass function](https://en.wikipedia.org/wiki/Weierstrass_function), which is differentiable nowhere, but continuous everywhere, thus measurable!

![The Weierstrass function, which is measurable.](https://upload.wikimedia.org/wikipedia/commons/thumb/6/60/WeierstrassFunction.svg/2880px-WeierstrassFunction.svg.png)

But it turns out that many discontinuous functions are also measurable. Let's look at one example: the *signum* function

$$\operatorname{sgn} : \mathbb R \to \mathbb R, \quad x \mapsto \begin{cases} 1, & x > 0 \\ 0, & x = 0 \\ -1, & x < 0 \end{cases}$$

(a friend-favourite, for some reason...). To show this, we need to show that for any Borel set $$A \subseteq \mathbb R$$, its preimage $$\operatorname{sgn}^{-1}(A) = \{x \in \mathbb R : \operatorname{sgn}(x) \in A\}$$ is again a Borel set in $$\mathbb R$$. One approach considers 8 cases; we do only one. Suppose that $$0,1 \in A$$ but $$-1 \not\in A$$. Then

$$\operatorname{sgn}^{-1}(A) = \{x \in \mathbb R : \operatorname{sgn}(x) \in A\} = \{x \in \mathbb R : \operatorname{sgn}(x) \in \{0,1\}\}$$

since $$\operatorname{sgn}$$ only takes on values in $$\{0,\pm 1\}$$. Therefore, $$\operatorname{sgn}^{-1}(A) = [0,\infty)$$; this is a Borel set since its complement is the open set $$(-\infty,0)$$ (and open sets are always Borel sets).

**Challenge question 5.** Complete the above proof that the signum function is measurable by identifying the remaining 7 cases, and checking that $$\operatorname{sgn}^{-1}(A)$$ is a Borel set in each case.

Going back to our example 9 with the uniform distribution on $$[0,1]$$, it now follows that the inclusion map $$X : \Omega \hookrightarrow \mathbb R, x \mapsto x$$, is a *random variable*, since it is continuous (thus measurable). This is how we typically think of a random variable with a uniform distribution!

Briefly, let's consider random variables from finite probability spaces. Since the natural sigma algebra is the power set, it follows that *every* function is measurable. So *any* function $$X : \Omega \to E$$ is a valid random variable. Let's now look at random variables in a bit more depth.

### Fun with random variables

Let's first introduce some notation. Recall that a random variable $$X : \Omega \to E$$ is a *measurable function* from a probability space $$(\Omega,\mathcal F,\mathbb P)$$ to a measurable space $$(E,\mathcal E)$$. It's not a *variable*! And it's not even random... the "randomness" comes from the fact that a probability measure assigns "chances" to different events. Let's now combine the notion of *random variable*, with the notion of *probability space*. This is how you've learnt random variables in high school/early university!

For the following, we take $$E = \mathbb R$$. Let $$A \subseteq \mathbb R$$ be a Borel set. Then since $$X$$ is measurable, $$X^{-1}(A)$$ is a valid event. Thus we may take its probability, and we write it in the following ways:

$$\mathbb P(X^{-1}(A)) = \mathbb P(\{\omega \in \Omega : X(\omega) \in A\}) = \mathbb P(X \in A).$$

Of these, the last is probably the most familiar. But they all mean the same thing! In fact, what we *mean* when we write $$X \in A$$, is precisely the event $$X^{-1}(A)$$!

**Example 8 (continued from part 1).** Recall this example, in which we had an infinite sequence of coin tosses and a sample space $$\Omega = \{0,1\}^\infty$$. For $$n \geq 1$$, consider the following random variable $$X_n : \Omega \to \mathbb R,$$

$$\omega = (\omega_1,\omega_2,...) \mapsto \omega_n,$$

which is simply projection onto the $$n$$th coordinate. For example, if $$n = 2$$ and we consider the outcome $$\omega = (1,0,1,0,...)$$, we get $$X_2(\omega) = 0$$. We can see that this essentially measures the outcome of the $$n$$th toss: if it was a tail, then $$X_n(\omega) = 0$$; if a head, then $$X_n(\omega) = 1$$. Assuming that each toss independently has probability $$p \in (0,1)$$ of appearing as a head, we observe the following: for any $$n$$,

$$\mathbb P(X_n = 1) = \mathbb P(X_n^{-1}(\{1\})) = \mathbb P(\{\omega \in \Omega : X_n(\omega) = 1\}) = p,$$

by our assertion. Similarly, $$\mathbb P(X_n = 0) = \mathbb P(\{\omega \in \Omega : X_n(\omega) = 0\}) = 1 - p$$, since

$$X_n^{-1}(0) \cup X_n^{-1}(1) = X_n^{-1}(\{0,1\}) = \Omega$$

and

$$X_n^{-1}(0) \cap X_n^{-1}(1) = X_n^{-1}(\{0\} \cap \{1\}) = X_n^{-1}(\varnothing) = \varnothing,$$

i.e. the two events $$\{X_n = 0\}$$ and $$\{X_n = 1\}$$ are disjoint (as expected), and their union is the sample space (this is called a **partition**), so the sum of the above two probabilities should be 1. (Note that here we use general properties of preimages of functions ($$f^{-1}(A \cup B) = f^{-1}(A) \cup f^{-1}(B)$$, $$f^{-1}(A \cap B) = f^{-1}(A) \cap f^{-1}(B)$$, and $$f^{-1}(A \setminus B) = f^{-1}(A) \setminus f^{-1}(B)$$), and when taking the preimage of a point, we often drop the curly brackets. It does *not* mean the inverse function; $$X_n$$ is certainly not invertible!)

**Example 9 (continued from part 1).** Let's again consider the uniform distribution on $$[0,1]$$, and the random variable $$X : \Omega \hookrightarrow \mathbb R, x \mapsto x$$ defined above. Then, for example, for $$(a,b) \subseteq (0,1)$$,

$$\mathbb P(a < X < b) = \mathbb P(X^{-1}((a,b))) = \mathbb P((a,b)) = b - a.$$

Now, recall that the composition of measurable functions is measurable, so if $$f$$ is for instance continuous, then $$f(X) = f \circ X$$ is also a random variable! Let's take $$f$$ to be the squaring function $$x \mapsto x^2$$. Let's investigate the random variable $$f(X) = X^2 : [0,1] \to \mathbb R$$ where $$X^2(\omega) = \omega^2$$:

**Challenge question 5 (related to example 9).**

1. Find $$(X^2)^{-1}(I) \subseteq [0,1]$$ for any open interval $$I = (a,b) \subseteq [0,1]$$. Is this a valid event (a Borel set in $$[0,1]$$)?
2. Thus compute the probability $$\mathbb P(a < X^2 < b)$$.
3. For $$x \in (0,1)$$, find $$(X^2)^{-1}((-\infty,x])$$ and thus find $$G(x) = \mathbb P(X^2 \leq x)$$. What is $$G(b) - G(a)$$?
4. Can you find a function $$g : (0,1) \to \mathbb R$$ such that $$\mathbb P(a < X^2 < b) = \int_a^b g(x)\,dx$$? (*Hint:* consider the function $$G : (0,1) \to [0,1]$$, and apply the *fundamental theorem of calculus*, which implies $$\int_a^b G'(x)\,dx = G(b) - G(a)$$.) This is (almost) the *probability density function* (or *pdf*) of $$X^2$$.

Post your solutions in the unofficial [Maths @ Monash Discord](https://discord.gg/hx63ZwSXBg)!

## Distributions: a change in perspective

### Probability distributions and pushforwards

A subtle but important change of perspective is to notice that for a probability measure $$\mathbb P$$ on the sample space, and a random variable $$X : \Omega \to E$$, we can actually define a *new* probability measure on the state space $$E$$, that arises naturally from $$X$$! This is the *pushforward measure* $$\mathbb P_X = X_*\mathbb P = \mathbb P \circ X^{-1} : \mathcal E \to [0,1]$$, defined by

$$\mathbb P_X(A) := \mathbb P(X^{-1}(A)) = \mathbb P(X \in A).$$

Here, $$A \in \mathcal E$$ is a (Borel) measurable set. Then the triple $$(E,\mathcal E,\mathbb P_X)$$ is a *probability space*, induced by the random variable $$X$$, so we can directly talk about probabilities using only the state space! And this is crucial in defining *probability distributions*, as we can then largely ignore the sample space!

This is something that we like to do a lot in maths: which is to start off with a structure on a set, and use a mapping to *transfer* that structure over to a different set. This is one such example; other examples of similar structure-preserving maps are continuous maps (preserving open sets), homeomorphisms (preserving topologies), isometries (preserving distances), linear transformations (preserving vector space structure), homomorphisms/isomorphisms (preserving algebraic structure), and pullbacks of bilinear forms under a linear map.

Now, let's consider $$(-\infty,x]$$ which is clearly a Borel set. We define the cumulative distribution function using the probability that $$X$$ takes on a value in this set:

**Definition 14.** For a random variable $$X : \Omega \to \mathbb R$$, its **(cumulative) distribution function (cdf)** is the measurable function $$F_X : \mathbb R \to [0,1]$$, defined by

$$F_X(x) = \mathbb P(X \leq x) = \mathbb P(X^{-1}((-\infty,x])) = \mathbb P_X((-\infty,x]).$$

That is, the cdf of $$X$$ gives us the probability measure of the event $$(-\infty,x]$$, where we push the probability measure from the sample space over to the state space! Similarly, if we have a probability space $$(\Omega,\mathcal F,\mathbb P)$$ with sample space $$\Omega \subseteq \mathbb R$$, we can define the **distribution function** of the probability measure $$\mathbb P$$ as $$F : \mathbb R \to [0,1]， x \mapsto \mathbb P((-\infty,x])$$.

As a quick note, the cdf of a random variable $$X$$ fully determines its properties, as we may recover the event $$X^{-1}(A) = \{X \in A\}$$ (thus $$\mathbb P(X \in A)$$) for any Borel set $$A$$ from countable unions/intersections/complements of events $$X^{-1}((-\infty,x]) = \{X \leq x\}$$ with $$x \in \mathbb R$$.

It is possible to see that any cdf must be *increasing* (i.e. if $$a < b$$, then $$F(a) \leq F(b)$$):

*Proof* For $$a < b$$, we have

$$F(b) = \mathbb P((-\infty,b]) = \mathbb P((-\infty,a] \cup (a,b]) = \mathbb P((-\infty,a]) + \underbrace{\mathbb P((a,b])}_{\geq 0} \geq F(a). \square$$

Additionally, cdfs have [*countably many discontinuities*](https://math.stackexchange.com/questions/147612/discontinuity-points-of-a-distribution-function), and must be *right-continuous*, meaning that not *every* increasing measurable function with codomain $$[0,1]$$ is the cdf of some random variable.

This change of perspective is useful, as it allows us to define when two random variables have the *same probability distribution*, even when they aren't defined on the *same probability space*! We say that two random variables $$X : (\Omega_1,\mathcal F_1,\mathbb P_1) \to (\mathbb R,\mathcal B)$$ and $$Y : (\Omega_2,\mathcal F_2,\mathbb P_2) \to (\mathbb R,\mathcal B)$$ are **equal in distribution** if their cdfs are equal as functions: $$F_X = F_Y$$; this means that $$\mathbb P_1(X \leq x) = \mathbb P_2(Y \leq x)$$ for all $$x \in \mathbb R$$ (note the different probability measures), or equivalently,

$$\mathbb P_X((-\infty,x]) = \mathbb P_Y((-\infty,x]),$$

which turns out to imply that $$\mathbb P_X = \mathbb P_Y$$ (the *pushforward measures*) as probability measures on the state space $$(\mathbb R,\mathcal B)$$ (again via the [Hahn-Kolmogorov theorem](https://handwiki.org/wiki/Hahn%E2%80%93Kolmogorov_theorem)). And hopefully this explains why the pushforward measure is so important: $$X$$ and $$Y$$ have the same probability distribution if and only if they induce identical probability spaces on the event space (via the pushforward measure), even if they are defined on totally different sample spaces.

### Examples of distributions

**Example 15.** Lets see an example of this, coming from our previous examples. Consider the first probability space to be the example with rolling two fair dice (independently) with $$\Omega_1 = \{1,...,6\} \times \{1,...,6\}$$, and the second probability space be the uniform distribution on $$\Omega_2 = [0,1]$$. Clearly these random variables are vastly different. Define the random variable $$X : \Omega_1 \to \mathbb R$$ as giving $$1$$ if the first die resulted in an equal or higher roll than the second, or $$0$$ otherwise:

$$X(\omega) = X((\omega_1,\omega_2)) = \begin{cases} 1, & \omega_1 \geq \omega_2 \\ 0, & \omega_1 < \omega_2 \end{cases}$$

Let $$Y : \Omega_2 \to \mathbb R$$ be given by the following transformation:

$$Y(\omega) = \begin{cases} 1, & \omega \leq 21/36 \\ 0, & \omega > 21/36 \end{cases}$$

Let's compute the cdfs of $$X$$ and $$Y$$. For $$X$$, for any $$x \in (-\infty,0)$$, we have $$X^{-1}((-\infty,x]) = \varnothing$$, so $$F_X(x) = \mathbb P_X((-\infty,x]) = \mathbb P_1(\varnothing) = 0$$. For $$x \in [0,1)$$, $$X^{-1}((-\infty,x]) = X^{-1}(0) = \{(\omega_1,\omega_2) \in \Omega_1 : \omega_1 \geq \omega_2\}$$, so

$$F_X(x) = \mathbb P_X((-\infty,x]) = \mathbb P_1(\{(\omega_1,\omega_2) \in \Omega_1 : \omega_1 \geq \omega_2\}) = \frac{21}{36}$$

by a simple combinatorial argument, and the fact that the 21 outcomes in that event are equiprobable. Now for $$x \in [1,\infty)$$, $$X^{-1}((-\infty,x]) = X^{-1}(\{0,1\}) = \Omega_1$$, so $$F_X(x) = \mathbb P_X((-\infty,x]) = \mathbb P_1(\Omega_1) = 1$$. In summary:

$$F_X(x) = \begin{cases} 0, & x < 0 \\ 21/36, & 0 \leq x < 1 \\ 1, & x \geq 1 \end{cases}$$

**Challenge question 6 (related to example 15).** Compute the cdf of $$Y$$, and show that $$X$$ and $$Y$$ are equal in distribution. (This then implies $$\mathbb P_X = \mathbb P_Y$$ and $$\mathbb P_1(X \in A) = \mathbb P_2(Y \in A)$$ for any Borel set $$A$$, and we may as well forget about the original sample spaces and consider the abstract properties of their common induced probability space on $$\mathbb R$$!) If you need a reminder of how $$(\Omega_2,\mathcal F_2,\mathbb P_2)$$ works, the example is Example 9 in [here](https://subjunctivequaver.github.io/posts/measure-theory-in-probability/).

At this point, we are finally ready to *define* discrete and continuous random variables, or more fundamentally, probability distributions.

**Definition 16.**

1. A **continuous random variable** $$X : \Omega \to \mathbb R$$ is such that $$\mathbb P(X = x) = \mathbb P_X(\{x\}) = 0$$ for all $$x \in \mathbb R$$.
2. An **absolutely continuous random variable** $$X : \Omega \to \mathbb R$$ is such that there exists a function $$f : \mathbb R \to [0,\infty]$$ such that $$\mathbb P(X \in A) = \int_A f(x)\,dx$$ for *any* Borel set $$A \subseteq \mathbb R$$. This function $$f$$ is the **probability density function (pdf)** of $$X$$. (Absolutely continuous random variables are continuous.)
3. A **discrete random variable** $$X : \Omega \to \mathbb R$$

Next up, to tackle the problem of densities, such as the normal pdf given at the start of part 1, we must consider a new form of integral: the Lebesgue integral. We leave this to the next part of this series!
