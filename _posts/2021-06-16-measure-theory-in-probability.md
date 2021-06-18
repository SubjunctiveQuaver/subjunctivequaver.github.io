---
title: Why probability and statistics need measure theory
date: 2021-06-16 21:57:00 +1000
categories: [Epic Maths Time, New Perspectives]
tags: [probability, measure-theory, statistics, topology]     # TAG names should always be lowercase
math: true
---

## Introduction to the problem

You may have encountered continuous probability distributions such as the normal distribution. It's often used to model things in the real world, and has nice statistical properties. You know the bell curve. But what you may not have seen is its formula: the *probability density function* (often shortened to just *density*),

$$f_\theta : \mathbb{R} \to \mathbb{R}, \quad x \mapsto \frac{1}{\sqrt{2\pi\sigma^2}}\exp\left(-\frac{(x - \mu)^2}{2\sigma^2}\right)$$

given a value of $$\theta = (\mu,\sigma^2) \in \Theta$$. In our case, $$\Theta = \mathbb{R} \times (0,\infty)$$; this is known as the *parameter space*.

![The probability density function of a normally distributed random variable.](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8c/Standard_deviation_diagram.svg/2880px-Standard_deviation_diagram.svg.png)

How does this relate to probability? Well, everything. We begin informally: suppose that $$X$$ is a continuous random variable with density $$f_\theta$$. The meaning of this is unimportant initially; think of $$X$$ as a "variable" that takes on values randomly (we will see that this is very much not a random variable *should* be). For a "reasonable" subset $$A \subseteq \mathbb{R}$$, let $$\mathbb{P}(X \in A)$$ denote the probability that $$X \in A$$, i.e. the probability of the event $$\{X \in A\}$$ (whatever that means). It turns out that, and as is often taught in a class in probability (even at high school level),

$$\mathbb P(X \in A) = \int_A f_\theta(x)\,dx = \int_A \frac{1}{\sqrt{2\pi\sigma^2}}\exp\left(-\frac{(x - \mu)^2}{2\sigma^2}\right)\,dx.$$

In fact, we are kind of working backwards. The probability density function is essentially defined to be a function such that integrating it over the desired subset yields the probability of $$X$$ taking on a value in that set. Now, what should $$A$$ be allowed to be? Should we allow *every* subset of the reals? In particular, if $$A = \{x_0\}$$ for some $$x_0 \in \mathbb{R}$$, the previous formula implies that $$\mathbb P(X = x_0) = 0$$, as an integral over a point. Should we allow this? Does that mean the event $$\{X = x_0\}$$ is impossible? It turns out it *is* possible, and that *measure theory* has the answer to all of these questions.

## Measure theory, with a probabilistic flavour

### Topologies and sigma algebras

Measure theory is essentially the theory of assigning sizes to sets, done rigorously. We will motivate probability spaces, which are measure spaces in which the "total size" is 1. But first, we define a *topology*; it turns out that it is intimately related to measures. (*Warning:* this subsection is rather technical, so feel free to skim over it; it's mostly here for background.)

**Definition 1.** Let $$\Omega$$ be a set, called the **sample space** in our context. A **topology** on $$\Omega$$ is a collection $$\tau$$ of subsets of $$\Omega$$ satisfying the following properties:

1. **(Whole and empty set)** The whole and empty sets are elements of the topology: $$\Omega \in \tau$$ and $$\varnothing \in \tau$$;
2. **(Closure under arbitrary unions)** For an indexed collection of sets $$(A_i)_{i \in I}$$ with each $$A_i \in \tau$$ (finite or infinite), their union $$\bigcup_{i \in I} A_i \in \tau$$ also;
3. **(Closure under finite intersections)** For an finite collection of sets $$A_1,A_2,...,A_n$$ with each $$A_i \in \tau$$, their intersection $$\bigcap_{i = 1}^n A_i \in \tau$$ also.

If $$\tau$$ is a topology on $$\Omega$$, then the pair $$(\Omega,\tau)$$ is a **topological space**, and the elements in the topology (subsets of $$\Omega$$) are called **open sets**. A set $$B$$ is **closed** if $$\Omega \setminus B$$ is open.

Yes, this is the *topology* in which donuts are the same as (homeomorphic to) coffee mugs!

![Classic image of a mug and torus morphing into each other, from Wikipedia.](https://upload.wikimedia.org/wikipedia/commons/2/26/Mug_and_Torus_morph.gif)

Let's look at a simple example of a topological space: the usual one $$(\mathbb{R},\tau)$$ on the reals. We define it via the open sets: a subset $$A \subseteq \mathbb{R}$$ is *open* if, for *each* point $$a \in A$$, there is an open interval $$I = (a - \epsilon,a + \epsilon)$$ (with $$\epsilon > 0$$) centred at $$a$$ that is wholly contained in $$A$$, i.e. $$I \subseteq A$$. For example, the set $$\mathbb{R}$$ is open: for $$a \in \mathbb{R}$$, we have $$(a - 1,a - 1) \subseteq \mathbb{R}$$. Additionally, the set $$(0,1)$$ is open: for $$a \in (0,1)$$, let $$\epsilon = \min(a,1 - a) \leq a,1 - a$$; note that $$0 = a - a \leq a - \epsilon$$ and $$a + \epsilon \leq a + (1 - a) = 1$$, so $$(a - \epsilon,a + \epsilon) \subseteq (0,1)$$. However, the set $$[0,1)$$ is not open: at $$a = 0$$, *every* open interval centred at $$0$$ goes "outside" of $$(0,1)$$. From these, we see that $$\mathbb R \setminus \mathbb R = \varnothing$$ and $$\mathbb R \setminus (0,1) = (-\infty,0] \cup [1,\infty)$$ are *closed*. A similar argument shows that $$[0,1]$$ is closed (its complement is open); this suggests that the *intervals* that are open sets are precisely the open intervals $$(a,b)$$, and those that are closed sets are precisely the closed intervals $$[a,b]$$ (where we allow infinity and $$a = b$$).

Now back to our question: which sets can we talk about probabilities of? Suppose that we only allowed open and closed sets. Then sets as simple as $$[0,1)$$ would be disallowed, but it seems quite reasonable to talk about the probability of $$\{0 \leq X < 1\}$$! Thus we introduce sigma algebras:

**Definition 2.** Let $$\Omega$$ be a set, called the **sample space** in our context. A **sigma algebra (of sets)** on $$\Omega$$ is a collection $$\mathcal F$$ of subsets of $$\Omega$$ satisfying the following properties:

1. **(Whole and empty set)** The whole and empty sets are elements of the sigma algebra: $$\Omega \in \mathcal F$$ and $$\varnothing \in \mathcal F$$ (we may omit one of these);
2. **(Closure under countable unions)** For an countable collection of sets $$(A_i)_{i = 1}^\infty$$ with each $$A_i \in \mathcal F$$, their union $$\bigcup_{i = 1}^\infty A_i \in \mathcal F$$ also;
3. **(Closure under complements)** If $$A \in \mathcal F$$, then its **complement** $$A^c := \Omega \setminus A \in \mathcal F$$.

If $$\mathcal F$$ is a sigma algebra on $$\Omega$$, then the pair $$(\Omega,\mathcal F)$$ is a **measurable space**, and the elements in the sigma algebra (subsets of $$\Omega$$) are called **measurable sets**; in the context of probability, we call them **events**.

Note that by de Morgan's laws, we also have closure under countable intersections: if $$A_1,A_2,... \in \mathcal F$$, then $$A_1^c,A_2^c,... \in \mathcal F$$; then $$\bigcup_{i = 1}^\infty A_i^c = \left(\bigcap_{i = 1}^\infty A_i\right)^c \in \mathcal F$$, so its complement $$\bigcap_{i = 1}^\infty A_i \in \mathcal F$$.

Now, what's an example of a sigma algebra on the reals? For this, essentially take our standard topology from above, and just force it to be a sigma algebra: this gives the *Borel sigma algebra*.

**Definition 3.** Let $$(\Omega,\tau)$$ be a topological space. The **Borel sigma algebra** $$\mathcal B = \mathcal B(\tau)$$ is the smallest sigma algebra containing $$\tau$$, in the sense that if $$\mathcal F$$ is a sigma algebra such that $$\tau \subseteq \mathcal F$$, then $$\mathcal B \subseteq \mathcal F$$. Elements of $$\mathcal B$$ are then called **Borel sets**.

For example, $$[0,1)$$ is a Borel set. Why? Notice that $$[0,1) = [(-\infty,0) \cup [1,\infty)]^c$$. Since $$(-\infty,0)$$ is open, it must be a Borel set (as the Borel sigma algebra contains the topology). Also, since $$(-\infty,1)$$ is open, it too is a Borel set; its complement $$[1,\infty)$$ is then a Borel set (by property 3 of sigma algebras). Then $$(-\infty,0) \cup [1,\infty)$$ is a Borel set as a countable union of Borel sets. Finally, its complement $$[0,1)$$ is a Borel set, as claimed.

**Challenge exercise 1:** using a similar approach, prove that the set of irrational numbers is a Borel set. (*Hint:* at some point, you may want to consider a union of singleton sets $$\{x_0\}$$ for certain $$x_0 \in \mathbb{R}$$.) Post your solutions in the unofficial [Maths @ Monash Discord](https://discord.gg/hx63ZwSXBg)!

Almost any "reasonable" set you can think of will (almost surely, with probability 1!) be a Borel set (come up with your own examples and prove it), and these turn out to be precisely one broad class of sets $$A$$ for which it makes sense to talk about the probability of the event $$\{X \in A\}$$. Now it's time to tie this all back to probability. But to do so, we may as well (finally, for some of you) define probability rigorously...

### Measure and probability spaces

We define a way to assign "sizes" to measurable sets. This is the essence of measure theory.

**Definition 4.** A **measure** on a measurable space $$(\Omega,\mathcal F)$$ is a function $$\mu : \mathcal F \to [0,\infty]$$ (yes, we include infinity), satisfying:

1. **(Null empty set)** $$\mu(\varnothing) = 0$$;
2. **(Countable additivity)** If $$(A_i)_{i = 1}^\infty$$ is a countable sequence of pairwise disjoint sets (i.e. $$A_i \cap A_j = \varnothing$$ for $$i \neq j$$), then
   $$\mu\left(\bigcup_{i = 1}^\infty A_i\right) = \sum_{i = 1}^\infty \mu(A_i)$$.

Then $$(\Omega,\mathcal F,\mu)$$ is a **measure space**. If we add the additional property that $$\mu(\Omega) = 1$$, then $$\mu$$ is a **probability measure**, and $$(\Omega,\mathcal F,\mu)$$ is a **probability space**. (In this case, we usually write $$\mathbb P$$ instead of $$\mu$$, so that $$(\Omega,\mathcal F,\mathbb P)$$ is a probability space; here, $$\mathcal F$$ is the **event space**, and its elements are **events**.)

For example, the *Lebesgue measure* $$\lambda$$ on $$\mathbb{R}$$ is a way to assign lengths to subsets of the reals in a sensible way: $$\lambda((0,1)) = \lambda([0,1]) = 1$$, $$\lambda((0,1) \cup (3,5]) = 3$$, $$\lambda(\{1,2,3,4,5\}) = \lambda(\mathbb{N}) = \lambda(\mathbb{Q}) = 0$$, $$\lambda(\mathbb{R}) = \lambda(\mathbb{R} \setminus \mathbb{Q}) = \infty$$, etc.

But now we turn our attention back to probability spaces. Let's unpack this definition, at least for probability measures. Firstly, a probability is a function from the *event space* to $$[0,\infty]$$ (in fact, we can see that its codomain is $$[0,1]$$, by the other properties). The probability of the empty set must be 0; this makes sense, as we always expect some outcome to occur in an experiment. The probability of the sample space is 1; again this makes sense, as the sample space is the set of all outcomes. Finally, the key property of probability is that for a (countable) sequence of pairwise *disjoint* events, often called **mutually exclusive** events, the probability of their union is the sum of their probabilities. Again, this is intuitive from elementary probability: if two events can't happen simultaneously, we should be able to add their probabilities to get the probability of their union.

Let's firstly try our hand at proving some simple results we know from probability, using our new axioms! Let $$(\Omega,\mathcal F,\mathbb P)$$ be *any* probability space.

**Proposition 5.** For disjoint (mutually exclusive) $$A,B \in \mathcal F$$, we have $$\mathbb P(A \cup B) = \mathbb P(A) + \mathbb P(B)$$.

*Proof.* Observe that the sequence $$A,B,\varnothing,\varnothing,...$$ is such that any two events are pairwise disjoint. Then using property 2 of measures,

$$\mathbb P(A \cup B) = \mathbb P(A \cup B \cup \varnothing \cup \dotsb) = \mathbb P(A) + \mathbb P(B) + \mathbb P(\varnothing) + \dotsb = \mathbb P(A) + \mathbb P(B),$$

where we use the fact that $$\mathbb P(\varnothing) = 0$$, i.e. property 1 of measures. $$\square$$

**Proposition 6.** For $$A \in \mathcal F$$, we have $$\mathbb P(A^c) = 1 - \mathbb P(A)$$.

*Proof.* Observe that $$A,A^c$$ are disjoint, and $$A \cup A^c = \Omega$$. Then by Proposition 5,

$$1 = \mathbb P(\Omega) = \mathbb P(A \cup A^c) = \mathbb P(A) + \mathbb P(A^c),$$

so $$\mathbb P(A^c) = 1 - \mathbb P(A)$$, as claimed. $$\square$$

**Challenge question 2.** Prove that for *any* $$A,B \in \mathcal F$$ (not necessarily disjoint), we have $$\mathbb P(A \cup B) = \mathbb P(A) + \mathbb P(B) - \mathbb P(A \cap B)$$. (*Hint:* decompose $$A \cup B$$ into two disjoint events in $$\mathcal F$$.)

### Examples of probability spaces

Note that the probability measure $$\mathbb P$$ is extremely abstract: once we have decided on a *sample space*, that is, a set of possible outcomes, *any* function $$\mathbb{P} : \mathcal F \to [0,1]$$ satisfying the above properties of a measure, defines a "probability" on $$\Omega$$. This probability may range from something usual, to something wild. We consider a few simple examples:

**Example 7 (rolling two independent fair dice).** Here, a possible sample space is $$\Omega = \{1,...,6\} \times \{1,...,6\}$$, i.e. ordered pairs of numbers in $$1,...,6$$. This naturally encodes the outcome of a sequence of two dice rolls. Now what are the valid events? Since the sample space has $$36$$ elements (and is finite), we may take $$\mathcal F = \mathcal P(\Omega)$$, the power set of the sample space; that is, every subset of $$\Omega$$ is a valid event. (You can check that this is indeed a sigma algebra on $$\Omega$$. How many events are there in total?)

Now we consider the probability measure $$\mathbb P : \mathcal F \to [0,1]$$. Note that every event $$A$$ is a (countable) union of individual outcomes $$\omega \in \Omega$$. By our assumption of fairness and independence (which gives symmetry), each of the 36 possible outcomes is assigned a measure of $$\frac{1}{36}$$, so that $$\mathbb P(\Omega) = 1$$. Thus, for $$A \in \mathcal F$$, its probability depends only on its cardinality: in fact,

$$\mathbb P(A) = \mathbb P\left(\bigcup_{\omega \in A} \{\omega\}\right) = \sum_{\omega \in A} \mathbb P(\{\omega\}) = \sum_{\omega \in A} \frac{1}{36} = \frac{|A|}{36};$$

this fully specifies the probability space in this experiment. (Note that in this derivation, we assumed that $$\mathbb P$$ was a probability measure, to get countable additivity.)

**Example 8 (independently tossing a sequence of coins).** Here, a possible sample space is $$\{0,1\}^\infty$$, the space of infinite sequences with terms in $$\{0,1\}$$, where we may associate $$0$$ with a tails, and $$1$$ with a heads. In this case, an appropriate [event space](https://math.stackexchange.com/questions/1457569/question-about-the-sigma-algebra-for-infinite-coin-toss) $$\mathcal F$$ is more complicated. For a finite binary string $$b = b_1\dotsb b_n$$, define

$$A_b = \{(b_1,b_2,...,b_n,x_{n+1},x_{n+2},...) : x_{n+1},x_{n+2},... \in \{0,1\}\}.$$

Then for natural $$n \geq 0$$, define $$\mathcal F_n := \{\varnothing,\Omega\} \cup \{A_b : b\ \text{is a binary string of length at most}\ n\}$$. For example, $$\mathcal F_2 := \{\varnothing,\Omega,A_0,A_1,A_{00},A_{01},A_{10},A_{11}\}$$. Define $$\mathcal F$$ as the smallest sigma algebra containing $$\bigcup_{n = 0}^\infty \mathcal F_n$$ (the union turns out to not be a sigma algebra, as seen [here](https://math.stackexchange.com/questions/1457569/question-about-the-sigma-algebra-for-infinite-coin-toss)). We need this construction, instead of the entire power set of $$\Omega$$, as there turn out to be subsets of $$\Omega$$ that [cannot be assigned a measure](https://math.stackexchange.com/a/1457657/) in a way that agrees with our definition!

Now suppose that for each toss, a head appears with probability $$p \in (0,1)$$. For integer $$n \geq 1$$, let $$B_n$$ be the event that the first head is tossed on the $$n$$th toss: then

$$B_n = \{(\underbrace{0,0,...,0,1}_{n\ \text{tosses}},x_{n+1},x_{n+2},...) : x_{n+1},x_{n+2},... \in \{0,1\}\};$$

this is precisely the event $$A_{00\dotsb 1}$$ defined above, so we know that $$B_n$$ is a valid event (i.e. $$B_n \in \mathcal F$$), by construction.

**Challenge question 3 (related to example 8).** If a random variable $$X$$ is defined on $$\mathbb{Z}^+$$ such that the event $$\{X = n\} = B_n$$ (i.e. $$\mathbb P(X = n) = \mathbb P(B_n)$$):

1. What is the well-known distribution of $$X$$?
2. Thus, what should $$\mathbb P$$ assign to this event $$B_n$$?
3. Show that each singleton set (containing a single sequence of tosses) is in the event space, so that it makes sense to talk about its probability. What is this probability of any individual sequence $$\omega = (x_1,x_2,...)$$ of tosses in $$B_n$$?
4. Is $$\mathbb P(B_n) = \mathbb P\left(\bigcup_{\omega \in B_n} \{\omega\}\right) = \sum_{\omega \in B_n} \mathbb P(\{\omega\})$$, and is this a contradiction, since the $$B_n$$ are pairwise disjoint and we expect the probability of the union to be the sum of the probabilities? (*Hint:* what is $$\lvert B_n \rvert$$? Can you show that it is *uncountable*? Consider Cantor's diagonalisation argument.)

Post your solutions in the unofficial [Maths @ Monash Discord](https://discord.gg/hx63ZwSXBg)!

In this previous example, we saw an example of an event with probability 0, but is certainly possible: of course, the event of any particular sequence of heads/tails is a possible outcome.

**Example 9 (uniform distribution on unit interval).** In this example, $$\Omega = [0,1]$$. Imagine randomly selecting a number in $$[0,1]$$; random number generators do this (pseudorandomly) all the time. What is the probability of getting a particular number $$\omega \in [0,1]$$? (We'll answer this later.) Let's firstly consider the event space. It turns out the power set of $$[0,1]$$ is too big (we cannot define a probability measure on it); this is where we use the *Borel sigma algebra*! Recall the Borel sets in $$\mathbb R$$. We say that $$A \subseteq [0,1]$$ is a Borel set (in $$[0,1]$$) if it is a Borel set in $$\mathbb R$$, under the usual topology (open sets contain open intervals about every point). So $$\mathcal F = \mathcal B$$; for example, $$[0,1],(0,1),(1/2,3/4),\mathbb Q \cap [0,1]$$ are all valid events.

We define $$\mathbb P : \mathcal F \to [0,1]$$ in a natural way: for any open interval $$I = (a,b) \subseteq [0,1]$$, we define $$\mathbb P(I) = b - a$$. Moreover, define $$\mathbb P([0,a)) = a$$ and $$\mathbb P((a,1]) = 1 - a$$ for $$a \in (0,1)$$. This then extends to all the other Borel sets via the properties of a probability measure (invoking the [Hahn-Kolmogorov theorem](https://handwiki.org/wiki/Hahn%E2%80%93Kolmogorov_theorem)). The intuition behind this is that probability should be proportional to the length/size, or *Lebesgue measure*, of the set. For example, the probability of $$A = \{0,1/2\}$$ is $$0$$: $$A^c = (0,1/2) \cup (1/2,1]$$. We defined $$\mathbb P((0,1/2)) = \mathbb P((1/2,1]) = 1/2$$. Therefore,

$$\mathbb P(A^c) = \mathbb P\left(\left(0,\frac{1}{2}\right) \cup \left(\frac{1}{2},1\right]\right) = \mathbb P\left(\left(0,\frac{1}{2}\right)\right) + \mathbb P\left(\left(\frac{1}{2},1\right]\right) = \frac{1}{2} + \frac{1}{2} = 1,$$

meaning that $$\mathbb P(A) = 0$$. Again, this is an event that is possible (we *can* pick $$0$$ or $$1/2$$ randomly, but the *probability* is $$0$$.)

As another example, we compute $$\mathbb P(\mathbb A \cap \Omega)$$, where $$\mathbb A \subseteq \mathbb C$$ is the set of algebraic numbers, i.e. roots of polynomials with *integer* coefficients. By the fundamental theorem of algebra, a degree $$n$$ polynomial has at most $$n$$ roots. By identifying the degree-$$n$$ polynomial $$p(x) = a_0 + a_1x + \dotsb + a_nx^n \in \mathbb Z[x]$$ with the sequence $$(a_0,a_1,...,a_n) \in \mathbb Z^n$$ and taking a union over all $$n \in \mathbb N$$, it is possible to see that the set of polynomials $$\mathbb Z[x]$$ with integral coefficients is [countable](https://math.stackexchange.com/questions/341349/prove-that-the-set-of-integer-coefficients-polynomials-is-countable). Thus there are at most a countable number of algebraic numbers (by counting the roots as you count these polynomials). As shown in the following challenge question, $$\mathbb P(\{x\}) = 0$$ for any $$x \in [0,1]$$. Since $$\mathbb A \cap \Omega$$ is a countable union of such singleton sets, it follows by countable additivity that $$\mathbb P(\mathbb A \cap \Omega) = 0$$.

**Challenge question 4 (related to example 9).**

1. Show, using only the properties of a probability measure, that for any $$x \in [0,1]$$, $$\mathbb P(\{x\}) = 0$$.
2. Thus show that $$\mathbb P([a,b]) = b - a$$ for *closed intervals* $$[a,b] \subseteq [0,1]$$ with $$a \neq 0$$ and $$b \neq 1$$ (although it is true for those too).
3. It is known that $$B = \sin^2(\mathbb N) = \{\sin^2(n) : n \in \mathbb N\}$$ (where $$0 \in \mathbb N$$) is dense in $$[0,1]$$ (meaning that you can find points in $$B$$ within *any* (possibly arbitrary small) open subinterval of $$[0,1]$$); find the probability that you do *not* randomly choose a number in $$B$$, i.e. $$\mathbb P(\Omega \setminus B)$$.

Post your solutions in the unofficial [Maths @ Monash Discord](https://discord.gg/hx63ZwSXBg)!

We've now had quite a bit of experience with probability spaces, and maybe you can start to appreciate the role of measure theory in probability! Now we are finally ready, and will attempt to answer the age-old question: what is a random variable?

### What is a random variable?

Let $$(\Omega,\mathcal F,\mathbb P)$$ be a probability space.

**Definition 10.** A **random variable** is a *measurable* function $$X : \Omega \to E$$, where $$(E,\mathcal E)$$ is the **state space**. We usually take $$E$$ to be a topological space $$(E,\mathcal T)$$ (e.g. $$\mathbb R,\mathbb R^n,\mathbb C$$ with the usual topologies), so that $$(E,\mathcal B)$$ is endowed with the *Borel sigma algebra*.

Clearly we must define measurable functions.

**Definition 11.** A function $$f : (\Omega,\mathcal F) \to (E,\mathcal E)$$ between measurable spaces is **measurable** if, for any measurable subset $$A \in \mathcal E$$ of $$E$$, its *preimage*

$$f^{-1}(A) := \{x \in \Omega : f(x) \in A\}$$

is measurable in $$\Omega$$, i.e. $$f^{-1}(A) \in \mathcal F$$.

For now, we will take $$\Omega = E = \mathbb R$$, and the Borel sigma algebra on $$\mathbb R$$. What are some examples of measurable functions? Well, it turns out that every function you can think of (well, with probability 1) will be measurable! One particularly nice class of measurable functions in this case are the *continuous functions*:

**Definition 12.** A function $$f : (\Omega,\tau) \to (E,\mathcal T)$$ between *topological spaces* is **measurable** if, for any open subset $$A \in \mathcal T$$ of $$E$$, its *preimage* $$f^{-1}(A)$$ is open in $$\Omega$$, i.e. $$f^{-1}(A) \in \tau$$.

Hopefully you can see the similarity: just replace "measurable" with "open"! Again, this may be different to the usual notion of continuity that you know (nearby inputs map to nearby outputs), but they turn out to be [equivalent](https://math.stackexchange.com/questions/2762135/equivalence-of-continuity-between-metric-and-topological-spaces). Here is a quick proof of the above claim:

**Proposition 13.** Suppose $$f : (\Omega,\tau) \to (E,\mathcal T)$$ is a *continuous* function. Then for a sigma algebra $$\mathcal F$$ on $$\Omega$$ that *contains* the Borel sigma algebra $$\mathcal B(\tau)$$, the function $$f : (\Omega,\mathcal F) \to (E,\mathcal B(\mathcal T))$$ is *measurable*.

*Proof.* Let $$A \in \mathcal B(\mathcal T)$$ be measurable

To be continued...

### Expected value: a Lebesgue integral?

To be continued...
