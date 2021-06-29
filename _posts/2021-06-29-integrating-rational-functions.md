---
title: Integrating rational functions, partial fractions, and a taste of algebra, part 1
date: 2021-06-29 15:42:00 +1000
categories: [Epic Maths Time, Cool Stuff]
tags: [algebra, calculus, rings, polynomials, uni-maths] # TAG names should always be lowercase
math: true
---

You know how to integrate a polynomial:

$$\int (a_0 + a_1x + \dotsb + a_nx^n) \,dx = C + a_0x + \frac{a_1}{2}x^2 + \dotsb + \frac{a_n}{n + 1}x^{n + 1},$$

where $$C \in \mathbb R$$ is a real constant. But what about a _rational function_ $$\frac{p}{q}$$ where $$p,q$$ are polynomials? Is the indefinite integral
$$\int \frac{p(x)}{q(x)}\,dx$$
a family of _elementary_ functions? It turns out that it is — that is, in theory at least, we can take any rational function and write its integral explicitly using "nice" functions (namely other rational functions, logarithms, and arctangents).

The key idea is to use polynomial division with remainder, and _partial fraction decomposition_. It might be obvious what the solution is now, but not so fast: have you ever thought about _how_ and _why_ partial fractions work? And can we do it without complex numbers in the (result of the) integral? Must the coefficients be real, or can they be complex too? And does this process perhaps... generalise? We will answer these questions (and more), by delving into the mysterious world of abstract algebra. (This will probably be the first of many posts on algebra, which is a field of maths that is close to my heart.)

## A quick recap on partial fractions

You may have previously learnt partial fractions to solve the problem of integrating certain rational functions (or simply plotting rational functions). More or less, the process looks like the following: we have a rational function (a quotient of polynomials)

$$\frac{p(x)}{q(x)}$$

where the degree of $$p$$ is strictly less than the degree of $$q$$. We then factorise $$q$$ into

$$q(x) = q_1(x)^{a_1} q_2(x)^{a_2} \dotsb q_k(x)^{a_k}$$

where typically the $$q_i$$ are _irreducible_ in the sense that there are no nontrivial factorisations of $$q_i$$ into a product of lower degree polynomials (and each $$a_i \in \mathbb Z^+$$). Then we can write

$$\frac{p(x)}{q(x)} = \sum_{j = 1}^{a_1} \frac{p_{1j}(x)}{q_1(x)^j} + \sum_{j = 1}^{a_2} \frac{p_{2j}(x)}{q_2(x)^j} + \dotsb + \sum_{j = 1}^{a_k} \frac{p_{kj}(x)}{q_k(x)^j}$$

where $$\deg p_{ij} < \deg q_i$$ for all $$i,j$$.

For example, for given $$a,b,c,d,e \in \mathbb R$$, we may decompose

$$\frac{ax^4 + bx^3 + cx^2 + dx + e}{x(x - 1)^2(x^2 + x + 1)} = \frac{A}{x} + \frac{B}{x - 1} + \frac{C}{(x - 1)^2} + \frac{Dx + E}{x^2 + x + 1}.$$

A usual technique is, once we have the correct form of the partial fraction decomposition, we cross-multiply to yield

$$ax^4 + bx^3 + cx^2 + dx + e = A(x - 1)^2(x^2 + x + 1) + Bx(x - 1)(x^2 + x + 1) + Cx(x^2 + x + 1) + (Dx + E)x(x - 1)^2,$$

which, considering as an equation in $$\mathbb R_4[x]$$ (the vector space of real polynomials of degree at most 4) and explicitly rewriting the right-hand side as a linear combination of basis polynomials $$x^4,x^3,x^2,x,1$$, allows us to compare coefficients and form a system of 5 equations in 5 variables, which must be consistent (as we will see in the existence of decomposition proof). Gaussian elimination (or another approach) then yields the unique coefficients $$A,B,C,D,E \in \mathbb R$$, at which point we have found the partial fraction decomposition.

### Partial fractions for... fractions?

Partial fractions for rational functions is something that most people have studied. But you may be more surprised to find out that the same process works if we replace the real number polynomial coefficients with _any_ other field (essentially a set with addition and multiplication, where you can divide by anything nonzero), e.g. the complex numbers, rationals, or integers modulo a prime! Perhaps even more surprisingly, we can do partial fractions for the _rational numbers_ $$\mathbb Q$$.

What exactly do I mean? We start off with a proper fraction (numerator is less than denominator). We can let _prime numbers_ take the place of irreducible (quadratic and linear) polynomials on the denominators, and instead of the condition that the degree of the numerator is strictly less than that of the irreducible polynomial in the denominator, we require that the _absolute value_ of the numerator is strictly less than that of the prime in the denominator. For example, I calculated that

$$\frac{37}{300} = \frac{1}{2} + \frac{1}{2^2} + \frac{1}{3} - \frac{4}{5} - \frac{4}{5^2}.$$

Why should this be the correct generalisation? In the proof of the existence of a partial fraction decomposition, we will see that we don't need to explicitly assume we are working with polynomials. In fact, the same argument works for any _Euclidean domain_, which is, roughly speaking, a set with addition, multiplication, and a null factor law, where we can also perform division with remainder (with a notion of size called a _valuation_). For real polynomials (which are building blocks of rational functions), the valuation is the degree function, but in the integers (which are building blocks of the rationals), a valuation is the _absolute value function_. The notion of an Euclidean domain is abstract algebraic, but allows us to abstract away from a concrete construction and prove results simultaneously for a general class of objects; furthermore, the algorithm in each Euclidean domain is _identical_, up to the actual division with remainder algorithm. And this is just a taste of the power of abstract algebra.

## Rings, fields, and Euclidean domains

This section will be a self-contained brief introduction to the relevant ring theory required for the proof. It may seem very definition heavy, and if you cannot follow, feel free to skip (at your own risk) to part 2. We firstly define rings.

**Definition 1.** A **binary operation** on a set $$X$$ is a map $$f : X \times X \to X$$ from the Cartesian product. It takes in two elements of $$X$$, and returns a single element, _also in_ $$X$$. We often write $$f(x,y) = x * y$$.

Some properties of a binary operation $$* : X \times X \to X$$ may include:

- **Commutativity:** for all $$x,y \in X$$, $$x * y = y * x$$. (Order doesn't matter.)
- **Associativity:** for all $$x,y,z \in X$$, $$(x * y) * z = x * (y * z)$$. (Brackets don't matter.)
- **Identity:** there is an $$e \in X$$ such that $$e * x = x * e = x$$ for all $$x \in X$$. (Applying $$e$$ doesn't do anything.)
- **Inverses:** if $$e$$ is the identity, then for any $$x \in X$$, there exists $$y \in X$$ such that $$x * y = y * x = e$$. (You can undo everything.)

For example, addition on $$\mathbb R$$ (but also $$\mathbb Z,\mathbb Q,\mathbb C$$) satisfies all 4 above criteria, with identity $$e = 0$$ and inverse $$y = -x$$ for $$x \in \mathbb R$$. (However, inverses is not satisfied if we take addition on $$\mathbb N$$; 1 has no inverse.) Multiplication (on $$\mathbb R$$) is commutative, associative, and has identity $$1$$. Subtraction is a binary operation, but is neither commutative nor associative, and has no identity! (Can you see why?)

**Challenge question 1.** Prove that on $$\mathbb R$$, subtraction is a binary operation that is not commutative, associative, and has no identity. Identify which of division on $$\mathbb R$$, exponentiation on $$\mathbb R^+$$, maximum on $$\mathbb R$$, and greatest common divisor on $$\mathbb Z^+$$ are binary operations, and which of the above properties they possess (if they are binary operations). Post your solutions in the unofficial [Maths @ Monash Discord](https://discord.gg/hx63ZwSXBg)!

**Definition 2.** A **(unital) ring** $$(R,+,{\cdot})$$ is a set $$R$$ with two binary operations $$+$$ (addition) and $$\cdot$$ (multiplication), satisfying:

- **(A1)** _Addition_ is **commutative**
- **(A2)** _Addition_ is **associative**
- **(A3)** _Addition_ has an **identity**, $$0$$ (called **zero**)
- **(A4)** Each element $$r \in R$$ has an **inverse** under _addition_, $$-r$$ (called the **negative**)
- **(M1)** _Multiplication_ is **associative**
- **(M2)** _Multiplication_ has an **identity**, $$1$$ (called **unity**)
- **(AM)** _Multiplication_ **distributes** over _addition_: for $$r,s,t \in R$$, $$r \cdot (s + t) = (r \cdot s) + (r \cdot t)$$ and $$(r + s)\cdot t = (r \cdot t) + (s \cdot t)$$

Properties (A1)–(A4) imply $$(R,+)$$ is an **abelian group**. Property (AM) implies multiplication and addition interact nicely. These properties are often called _axioms_. Additionally, multiplication takes precedence over addition, i.e. $$r \cdot s + t = (r \cdot s) + t$$ and $$r + s \cdot t = r + (s \cdot t)$$. (We often drop the $$\cdot$$ when performing multiplication, and write $$rs = r \cdot s$$.) Rings in which multiplication is also commutative are the creatively-named **commutative rings**.

Some examples of (unital) rings include $$\mathbb R,\mathbb C,\mathbb Q,\mathbb Z$$ under the usual addition and multiplication (with zero $$0$$ and unity $$1$$), continuous functions under the usual pointwise addition and multiplication, the set of $$n \times n$$ square matrices $$M_n(R)$$ over a ring $$R$$ (with zero the zero matrix, and unity the identity matrix with the unity from $$R$$ down the diagonal and zeroes elsewhere; here, multiplication is _not commutative!_), and polynomial rings (which we discuss later).

**Definition 3.** A **unit** in a (unital) ring (with unity $$1$$) is an element $$u \in R$$ such that there exists $$v \in R$$ with $$uv = vu = 1$$; then $$v = u^{-1}$$ is a **(multiplicative) inverse** of $$u$$. The set of units in $$R$$ is denoted $$R^*$$; it is a group (it satisfies precisely (A2)–(A4) plus closure, but for multiplication instead), called the **unit group**.

**Challenge question 2.**

1. Prove, using the axioms only, that the zero $$0$$ and unity $$1$$ are unique in a ring.
2. Thus prove that if additive or multiplicative inverses exist, then they are unique.
3. Prove that $$R^* := \{u \in R : u\ \text{is a unit}\}$$ forms a group under multiplication from $$R$$. (That is, multiplication is a binary operation (i.e. the product of two units is a unit), it is associative, has an identity, and every element has an inverse.)

**Challenge question 3.** Let us consider the ring of $$2 \times 2$$ integer matrices $$M_2(\mathbb Z)$$, endowed with the usual addition and multiplication of square matrices (from say $$M_2(\mathbb R)$$).

1. Argue that if

   $$A = \begin{pmatrix} a & b \\ c & d \end{pmatrix} \in M_2(\mathbb Z)$$

   has a (multiplicative) inverse $$A^{-1} \in M_2(\mathbb Z)$$ such that $$AA^{-1} = A^{-1}A = I$$ (where $$I$$ is the usual $$2 \times 2$$ identity matrix), then

   $$A^{-1} = \frac{1}{ad - bc} \begin{pmatrix} d & -b \\ -c & a \end{pmatrix} \in M_2(\mathbb R)$$.

2. Thus conclude that $$A \in M_2(\mathbb Z)$$ has an inverse if and only if $$\det A \in \{\pm 1\} = \mathbb Z^*$$. This proves that the unit group is $$GL_2(\mathbb Z) := (M_2(\mathbb Z))^* = \{A \in M_2(\mathbb Z) : \det A = \pm 1\}$$.
3. Use this to conjecture what $$GL_n(\mathbb Z) := (M_n(\mathbb Z))^*$$ is, for any integer $$n \geq 1$$.
4. Prove that for _any_ commutative (unital) ring $$R$$ (where multiplication is commutative), $$GL_2(R) := (M_2(R))^* = \{A \in M_2(R) : \det A \in R^*\}$$, where the determinant is defined as usual. This is the **general linear group**: the set of invertible matrices with entries in $$R$$. (Compare this to what you know when $$R = \mathbb R$$ or $$\mathbb C$$.)

Post your solutions in the unofficial [Maths @ Monash Discord](https://discord.gg/hx63ZwSXBg)!

### Fields, division rings, and the quaternions

**Definition 4.** A **field** $$F$$ is a commutative (unital) ring such that $$F^* = F \setminus \{0\}$$, that is, every nonzero element has a (multiplicative) inverse. (It follows that $$F \setminus \{0\}$$ is an abelian group under multiplication.)

Some examples of fields include $$\mathbb R,\mathbb C,\mathbb Q$$, and also the integers modulo $$p$$ where $$p$$ is prime: $$\mathbb Z_p$$. Fields are also the building blocks of linear algebra: the scalars in a vector space belong to a field. If we remove the condition that the ring is commutative (but maintain the requirement that $$F^* = F \setminus \{0\}$$), we get a **skew-field** or **division ring**: a prominent example is $$\mathbb H$$, the **quaternions**, which is a 4-dimensional $$\mathbb R$$-vector space with (abstract) basis elements $$1,i,j,k$$ with multiplication satisfying $$1\alpha = \alpha 1 = \alpha$$ for all $$\alpha \in \mathbb H$$, and

$$i^2 = j^2 = k^2 = ijk = -1.$$

**Challenge question 4.** We work with the quaternions $$\mathbb H$$. Recall that we define multiplication so that it is a ring.

1. Show that $$ij = k$$, $$jk = i$$, $$ki = j$$, $$ji = -k$$, $$kj = -i$$, and $$ik = -j$$. (Think of this with $$ijk$$ written cyclically, with a negative sign if we go backwards.) What is $$i^{-1}$$, $$j^{-1}$$, and $$k^{-1}$$?
2. For a quaternion $$\alpha = a + bi + cj + dk \in \mathbb H$$ (where $$a,b,c,d \in \mathbb R$$) and $$\lambda = \lambda + 0i + 0j + 0k \in \mathbb R$$, show that $$\lambda\alpha = \alpha\lambda$$. (Hint: $$\lambda = \lambda 1$$, and use associativity.)
3. For $$\alpha = a + bi + cj + dk \in \mathbb H$$ (where $$a,b,c,d \in \mathbb R$$), define $$\bar\alpha = a - bi - cj - dk$$. Define the **norm** $$N(\alpha) = \alpha\bar \alpha$$. Expand to show that $$N(\alpha) \in \mathbb R$$ (using distributive laws, and parts 1 & 2).
4. Prove that $$N(\alpha\beta) = N(\alpha)N(\beta)$$ for $$\alpha,\beta \in \mathbb H$$, and that $$N(\alpha) = 0$$ if and only if $$\alpha = 0$$.
5. If $$\alpha \neq 0$$, Let $$\beta = \bar\alpha/N(\alpha)$$. What is $$\alpha\beta$$ and $$\beta\alpha$$? Thus conclude that $$\mathbb H^* = \mathbb H \setminus \{0\}$$, i.e. that $$\mathbb H$$ is a division ring.

Post your solutions in the unofficial [Maths @ Monash Discord](https://discord.gg/hx63ZwSXBg)!

**Definition 5.** SUBRINGS/SUBFIELDS

### Euclidean domains and the Euclidean algorithm

Valuations, gcds, Euclidean algorithm, etc

To be continued...

Make sure you read part 2, which can be found here soon.
