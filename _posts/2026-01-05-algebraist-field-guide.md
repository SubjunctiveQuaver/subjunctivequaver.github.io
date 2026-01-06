---
title: An algebraist’s field guide to constructing ℤ, ℚ, ℝ, ℂ, ℍ and 𝕆
date: 2026-01-06 01:20:00 +1100
categories: [Epic Maths Time, Just for Fun]
tags: [maths, uni-maths, algebra, ring-theory, frameworks, ai] # TAG names should always be lowercase
math: true
---

Mathematicians have constructed a small but diverse ecosystem of number systems, ranging from the integers (whole numbers) to the complex numbers and beyond. Even long after university (and now through YouTube), this post arose from a recurring *holy discontent* I feel as someone with an algebraic background -- a discontent that sounds roughly like this:

- Why did the Dedekind cut construction of the real numbers in analysis class make me want to cry?
- Aren't we essentially just [quotienting out null sequences from the Cauchy sequences](#3b-cauchy-completion-the-algebraic-version)? (Anyone else? No? Just me?)
- Why is everyone taking the rational numbers so much for granted?
- Why does everyone seem to love defining complex numbers as... ordered pairs of reals?
- Why don't more people talk about the [beautiful polynomial quotient construction of complex numbers](#4a-polynomial-quotient-my-favourite)? (Genuine question!)
- Isn't everything just quotienting and universal properties at the end of the day? (Stopping before I have to start learning category theory.)

With that in mind, we'll walk through some standard ways of building the main number systems in this *field* guide -- from the ring $\mathbb{Z}$, through *fields* (haha) $\mathbb{Q}$, $\mathbb{R}$ and $\mathbb{C}$, to the division algebras $\mathbb{H}$ and $\mathbb{O}$ -- with a distinctive algebraic flavour, noting what each construction buys you and what it costs. Read this post at your level. The constructions are there if you want them -- the mathematician opinions are there if you don't. One attribution: this post benefited from conversations with an AI assistant who is very patient with algebraists.

Along the way, we'll pause to notice how different mathematicians tend to react as constructions are made and familiar rules begin to slip. Algebraists, analysts, geometers and category theorists value different kinds of structure, and tolerate different kinds of failure. We'll keep a playful eye on these reactions as we go -- with category theorists, as ever, remaining slightly off to one side. Let's first meet the main characters.

---

## The main characters: 4 stereotypes of pure mathematicians

### Algebraist

*INTJ / ISTJ · 'There is a correct abstraction, and I will find it.'*

**Fields of study:**\\
Group, ring and field theory, algebraic number theory.

**What they love:**\\
Clean definitions, minimal constructions, quotients that feel inevitable, and objects characterised by what they *are*, not how they're built. Deeply satisfied by constructions that work uniformly and don't depend on arbitrary choices.

**What they dislike:**\\
Ad hoc definitions, unnecessary case distinctions, and proofs that devolve into epsilon–delta bookkeeping. Mildly suspicious of analysis, deeply suspicious of anything that works only 'up to convergence'.

**Stereotype:**\\
Quietly rewriting your definition until it becomes canonical -- and then pretending that was the plan all along.

### Analyst

*ISTJ / ISFJ · 'Does it converge?'*

**Fields of study:**\\
Real and complex analysis, functional analysis, PDEs, measure theory.

**What they love:**\\
Limits, completeness, continuity, and constructions that guarantee good behaviour. Sequences that converge, functions that behave, and proofs that come with explicit control.

**What they dislike:**\\
Gaps, discontinuities, and definitions that don't come with convergence guarantees. Uneasy around purely algebraic constructions until someone proves they're complete.

**Stereotype:**\\
Nodding politely at your construction, then asking whether it's complete.

### Geometer

*INFP / ENFP · 'Can I draw it?'*

**Fields of study:**\\
Differential geometry, topology, algebraic geometry, geometric group theory.

**What they love:**\\
Smoothness, symmetry, spatial intuition, and constructions that produce meaningful shapes and transformations. Objects that live naturally in space and do something interesting there.

**What they dislike:**\\
Pathological examples, excessive abstraction, and structures that stubbornly refuse to look like anything. Quietly resentful of counterexamples invented purely to cause trouble.

**Stereotype:**\\
Explaining something perfectly rigorous while gesturing vaguely in the air.

### Category theorist

*INTP · 'This is really about the arrows.'*

**Fields of study:**\\
Category theory, higher categories, topos theory.

**What they love:**\\
Universal properties, functoriality, and constructions that slot neatly into a broader framework. Deep satisfaction when many problems turn out to be the same problem. I don't know what most of this means.

**What they dislike:**\\
Special cases, ad hoc definitions, and anything that doesn't quite fit the vibe. Increasingly impatient with concrete models.

**Stereotype:**\\
Patiently waiting for everyone else to realise they were doing category theory all along.

---

## Building up: the simple picture

Before we get technical, it helps to see why each new number system was invented in the first place. We start with the numbers we can count.

**The integers $\mathbb{Z}$ -- counting and direction**\\
These are the numbers you get by counting forwards and backwards. They're great for keeping score, measuring steps and talking about direction. But they're rigid: you can't divide freely, and there's no notion of 'in between'.

So we add fractions. (We'll answer how later.)

**The rational numbers $\mathbb{Q}$ -- cutting things up**\\
Rationals let us divide things evenly. You can share, average, and compare proportions. They're dense -- there's always another rational between two others -- but they're still full of holes. Some lengths and limits just aren't there.

So we fill in the gaps. (We'll answer how later.)

**The real numbers $\mathbb{R}$ -- no missing points**\\
The real numbers complete the line. Every limit you expect to exist does exist. You can do calculus, talk about continuity, and trust that zooming in forever won't reveal a crack. This is where analysis feels at home.

Then someone asks what happens if we solve equations that shouldn't have solutions. (We'll answer how later.)

**The complex numbers $\mathbb{C}$ -- turning sideways**\\
Complex numbers add a new direction. Suddenly every polynomial has roots, rotations become multiplication, and calculus becomes smoother and more powerful. What looked artificial at first turns out to be very natural.

Then geometry gets ambitious. (We'll answer how later.)

**The quaternions $\mathbb{H}$ -- rotations in space**\\
Quaternions give a clean way to describe rotations in three dimensions. You lose commutativity, but gain elegance and stability. They're less about numbers on a line and more about how objects move.

Finally, curiosity wins. (We'll answer how later.)

**The octonions $\mathbb{O}$ -- what if we keep going?**\\
Octonions push the pattern one step further. You lose associativity, intuition, and most familiar tools -- but gain deep connections to exceptional geometry and symmetry. This is where structure starts to fray.

---

Now, let's dive into the constructions, one number system at a time. Read the following sections (numbered 1 to 6) at your level. The constructions are there if you want them -- the mathematician opinions are there if you don't.

## 1. The integers (ℤ)

The natural numbers $\mathbb{N} = \{0, 1, 2, \ldots\}$ are what we use to count. But, lacking negatives, we cannot solve equations like $x + 3 = 0$ within $\mathbb{N}$. Solving this equation would require $x = -3$, which is not a natural number. This leads us to the integers, which are closed under addition and subtraction (as well as multiplication).

**In real life:** This situation arises when we owe someone money. We can have \\$0 or a positive balance, but owing \\$3 means we'd have --\\$3.

### ℤː Construction

Grothendieck group completion of the monoid $(\mathbb{N}, +)$ of natural numbers.

**Formally:** $\mathbb{Z} = \mathbb{N} \times \mathbb{N} / \sim$, under the equivalence relation $(a,b) \sim (c,d)$ if $a + d = b + c$. The resulting object is an abelian group under the operation on equivalence classes:

$$[(a,b)] + [(c,d)] = [(a + c, b + d)]$$

**Intuition:** Represent an integer as 'a pile of counters minus another pile'.

### ℤː How mathematicians feel about it

- **Algebraists:** Deeply satisfied. This is the Platonic ideal of a construction -- minimal, canonical and doing exactly one job perfectly.
- **Analysts:** 'Sure, fine. Discrete scaffolding. Necessary, but only interesting insofar as it leads to limits.'
- **Geometers:** 'The fundamental group of a circle, but flattened and stripped of personality.' (They appreciate it conceptually, but would rather be drawing something.)
- **Category theorists:** 'Ah yes, the initial object in the category of rings. Everything begins here. Delicious.'

---

## 2. The rationals (ℚ)

The integers are closed under addition, subtraction and multiplication, but not division. We cannot solve equations like $3x = 2$ within $\mathbb{Z}$. Solving this equation would require $x = 2/3$, which is not an integer. This leads us to the rational numbers, which are closed under division except for division by zero.

**In real life:** This situation arises when we split things. Sharing 2 pizzas between 3 people would require each person to have 2/3 of a pizza.

### ℚ: Construction

There are 2 classic constructions:

#### (2A) Equivalence classes of pairs

Define $\mathbb{Q}$ as equivalence classes of pairs $(a,b)$ with $a \in \mathbb{Z}$ and $b \in \mathbb{Z} \setminus \\{0\\}$, where $(a,b) \sim (c,d)$ if $ad = bc$. Then define addition and multiplication by:

$$[(a,b)] + [(c,d)] = [(ad + bc, bd)]$$

$$[(a,b)] \cdot [(c,d)] = [(ac, bd)]$$

Then magically, every nonzero element has a multiplicative inverse: $[(a,b)]^{-1} = [(b,a)]$ for $a \neq 0$.

**Intuition:** Represent a rational number as a fraction $(a/b)$, but formally as an equivalence class to handle different representations of the same number.

#### (2B) Field of fractions

$\mathbb{Q}$ is the field of fractions of the integral domain $\mathbb{Z}$.

Formally, it is the universal field containing $\mathbb{Z}$ such that every nonzero element of $\mathbb{Z}$ becomes invertible.

This construction emphasizes the universal property: any injective ring homomorphism from $\mathbb{Z}$ to a field factors uniquely through $\mathbb{Q}$.

### ℚ: How mathematicians feel about it

- **Algebraists:** 'A perfect localisation. Crisp. Clean. Canonical. Like a well-oiled machine that never jams.'
  1. **Field of fractions:** 'The gold standard. Everything works exactly as it should. Effortless, inevitable and deeply satisfying.'
  2. **Equivalence classes of pairs:** 'The classic fraction construction -- concrete and serviceable, but clearly a model rather than the point.'
- **Analysts:** 'Finally, numbers I can put in a sequence without tripping over equivalence relations.'
  1. **Equivalence classes of pairs:** 'Feels like fractions you learned in school -- concrete, familiar and numerically behaved.'
  2. **Field of fractions:** 'Abstract but useful -- mainly appreciated for what it lets you embed into later.'
- **Geometers:** 'Points on a line, but only the ones with nice coordinates. Like a VIP guest list for the number line.'
  1. **Field of fractions:** 'The coordinate‑field viewpoint fits geometric intuition -- smooth, structural and embedding‑friendly.'
  2. **Equivalence classes of pairs:** 'More combinatorial, less geometric -- like trying to draw a line using bookkeeping.'
- **Category theorists:** 'The initial field containing $\mathbb{Z}$. Also a localisation. Also a colimit. Also a vibe. Basically the Beyoncé of number constructions.'
  1. **Field of fractions:** 'Pure universal property. Everything factors. Everything commutes. Perfection.'
  2. **Equivalence classes of pairs:** 'A concrete presentation -- fine, but why are we still talking about representatives?'

---

## 3. The reals (ℝ)

The rationals are a field: closed under addition, subtraction, multiplication and division (except by zero). However, they are not complete. We cannot solve equations like $x^2 = 2$ within $\mathbb{Q}$. Solving this equation would require $x = \sqrt{2}$, which is not a rational number.

This failure is not specific to $\sqrt{2}$, nor even to algebraic numbers -- roots of polynomials with integer coefficients. It reflects a deeper structural gap: $\mathbb{Q}$ is not closed under limits. There are sequences in $\mathbb{Q}$ that ought to converge but don't in $\mathbb{Q}$ -- familiar examples include sequences converging to transcendental numbers such as $\pi$ and $e$. Addressing this leads us to the real numbers, which form the unique complete ordered field.[^1]

[^1]: The field $\mathbb{Q}(\sqrt{2}) = \\{a + b\sqrt{2} : a,b \in \mathbb{Q}\\}$ does contain $\sqrt{2}$, but it is still not complete. In fact, adding every real algebraic number to $\mathbb{Q}$ still results in a field that is not complete. Completeness is about closing the field under limits: every Cauchy sequence must converge.

**In real life:** This situation arises when we measure distances 'as the crow flies'. If you walked 1&nbsp;km east and then 1&nbsp;km north, the straight-line distance back to your starting point is $\sqrt{2}$&nbsp;km -- not a rational number.

### ℝ: Construction

There are 2 classic constructions:

#### (3A) Dedekind cuts

Downward-closed subsets of $\mathbb{Q}$ with no greatest element, encoding a real number by everything less than it.

Analysts love this because it smells like order completeness.

#### (3B) Cauchy completion (the algebraic version!)

Consider the ring $\mathbb{Q}^{\infty}$ of all sequences $(x_n)_{n=1}^{\infty}$ with $x_n \in \mathbb{Q}$.

Define the subring $\mathcal{C}(\mathbb{Q}) \subseteq \mathbb{Q}^{\infty}$ consisting of all Cauchy sequences, i.e. sequences $(x_n)$ such that for every $\varepsilon > 0$, there exists $N$ with $\|x_m - x_n\| < \varepsilon$ for all $m,n \ge N$. These are sequences whose terms eventually become arbitrarily close to each other -- that may or may not converge in $\mathbb{Q}$.

Inside $\mathcal{C}(\mathbb{Q})$, define the ideal of null sequences:

$$\mathcal{N}(\mathbb{Q}) = \{ (x_n) \in \mathcal{C}(\mathbb{Q}) : x_n \to 0 \text{ as } n \to \infty \}$$

The quotient ring $\mathcal{C}(\mathbb{Q}) / \mathcal{N}(\mathbb{Q})$ is a field, which we identify with $\mathbb{R}$.

A real number $x \in \mathbb{R}$ corresponds to the equivalence class $(x_n) + \mathcal{N}(\mathbb{Q}) \in \mathcal{C}(\mathbb{Q}) / \mathcal{N}(\mathbb{Q})$, where $x_n \to x$ as $n \to \infty$. For example, one may take $x_n$ to be a rational approximation to $x$ accurate to $n$ decimal places.

**Intuition:** We complete $\mathbb{Q}$ by adding limits of Cauchy sequences, identifying sequences that differ by a null sequence. (The ideal $\mathcal{N}(\mathbb{Q})$ is maximal in $\mathcal{C}(\mathbb{Q})$, ensuring the quotient is a field.)

This construction blends algebraic structure with analytic completeness, capturing the essence of real numbers as limits of rational approximations. In other words: analysis isn't scary when it knows what it's trying to do. It just hands algebra the right inequality and steps aside.

### ℝ: How mathematicians feel about it

- **Algebraists:** Completion under a valuation. Very respectable. Quietly powerful. Preferences for algebraic numbers notwithstanding.
  1. **Cauchy completion:** The algebraic flavour appeals. Structure first -- epsilons only when absolutely necessary.
  2. **Dedekind cuts:** Order‑theoretic and correct, but feels orthogonal to how algebra wants to think.
- **Analysts:** 'Finally, limits exist.'
  1. **Dedekind cuts:** Intuitive and order-based. Encodes the axiom of completeness directly via suprema.
  2. **Cauchy completion (sequence version):** Familiar and operational. Every Cauchy sequence converges -- what more do you want?
  3. **Cauchy completion (algebraic version):** 'Please don't. I believe you -- I just don't want to see it. I don't need quotients or ring language to know that limits exist.'
- **Geometers:** 'A complete line. Smooth. Continuous. Lovely.'
  1. **Dedekind cuts:** The order structure feels geometric. But they just want a line they can draw.
  2. **Cauchy completion:** Algebraic but less geometric. But they just want a line they can draw.
- **Category theorists:** 'The terminal Archimedean complete ordered field. Also a completion. Also a reflective subcategory.' *Walks away mysteriously.*
  1. **Cauchy completion:** Completion and reflection are categorical wins.
  2. **Dedekind cuts:** Order‑theoretic, correct, but less universal‑property‑forward.

---

## 4. The complex numbers (ℂ)

The real numbers are a complete field: closed under arithmetic operations, closed under limits. But we cannot solve equations like $x^2 = -1$ within $\mathbb{R}$. Solving this equation would require $x = \sqrt{-1}$, which is not a real number. This failure is about algebraic closure: certain polynomial equations simply have no real solutions. Addressing this leads us to the complex numbers.

**In real life:** There is no real-life application of complex numbers (that is a joke). Complex numbers appear naturally in physics, engineering and signal processing.

### ℂ: Construction

Several classic constructions give us the complex numbers, each illuminating a different aspect:

#### (4A) Polynomial quotient (my favourite!)

*This is my favourite construction of the complex numbers, and it's the reason I wrote this post in the first place -- to hopefully raise awareness of the beauty of algebraic constructions through quotients.*

Consider the polynomial ring

$$\mathbb{R}[x] = \\{a_0 + a_1 x + \cdots + a_n x^n : n \in \mathbb{N} \text{ and each } a_i \in \mathbb{R}\\}$$

Form the quotient by the maximal ideal generated by $x^2 + 1$, i.e., $\mathbb{C} \cong \mathbb{R}[x]/(x^2 + 1)$.

A complex number $z = a + bi \in \mathbb{C}$ corresponds to the equivalence class of the polynomial $a + bx$ modulo $x^2 + 1$, where $i$ is identified with $x$ modulo $x^2 + 1$ in the quotient. Arithmetic proceeds as usual, with the relation $x^2 = -1$ used to simplify expressions.

This algebraic construction adds a root of the polynomial $x^2 + 1$ to $\mathbb{R}$, producing the smallest field extension where this polynomial factors.

**Intuition:** By forcing $x^2 + 1 = 0$, we create a new element $i$ with $i^2 = -1$, just like in high school. We don't need to define any other rules -- from this relation and properties of polynomial arithmetic, the other algebraic properties of $i$ and $\mathbb{C}$ follow naturally. And that's the beauty of this construction.

This construction also generalises to other field extensions in a straightforward way, including finite fields. See this Michael Penn video for a great explanation and more detail on how to make new fields (but not a *good place to stop* reading this post). He notes that $\mathbb{R}(i) = \mathbb{C}$ is a basic example -- and to me, this *is* the way to define the complex numbers.

<iframe width="560" height="315" src="https://www.youtube.com/embed/YSdidFMwn14?si=vddePzx9iZqss-kD" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

#### (4B) Ordered-pair model

Represent complex numbers as pairs $(a, b) \in \mathbb{R}^2$ with $a, b \in \mathbb{R}$.

- Define addition component-wise: $(a, b) + (c, d) = (a + c, b + d)$.
- Define multiplication by $(a, b)(c, d) = (ac - bd, ad + bc)$.

This matches the polynomial quotient construction by identifying $(a, b)$ with $a + bi$, with the operations explicit in coordinates.

#### (4C) Matrix model

Identify $a + bi$ with the $2 \times 2$ real matrix:

$$\begin{pmatrix} a & -b \\ b & a \end{pmatrix} \in M_2(\mathbb{R})$$

Matrix addition and multiplication correspond to complex addition and multiplication. So $\mathbb{C}$ embeds as a subring of $M_2(\mathbb{R})$.

**Intuition:** This model highlights the geometric interpretation of complex numbers as certain linear transformations (rotations and scalings) of the plane.

#### (4D) Algebraic closure of $\mathbb{R}$

This is a non-constructive approach: we define $\mathbb{C}$ as the algebraic closure of $\mathbb{R}$, meaning every non-constant polynomial with real coefficients factorises completely over $\mathbb{C}$.

This property makes $\mathbb{C}$ algebraically complete and fundamental in algebra and analysis.

### ℂ: How mathematicians feel about it

- **Algebraists:** 'A perfect quadratic extension, elegantly adding a root of $x^2 + 1$. The algebraic closure of $\mathbb{R}$ is the ultimate prize.'
  1. **Polynomial quotient:** 'Elegant and algebraically satisfying -- like a fine wine paired with a proof.'
  2. **Algebraic closure:** 'The grand finale -- the algebraic party where every polynomial shows up.'
  3. **Ordered-pair model:** 'Concrete and familiar -- like your favourite comfy chair.'
  4. **Matrix model:** 'Geometric and visual -- the artsy cousin.'
- **Analysts:** 'Holomorphic functions are magic, and $\mathbb{C}$ is where the magic works.'
  1. **Ordered-pair model:** 'Intuitive and analytic -- like a warm bath for your brain.'
  2. **Matrix model:** 'Geometric insight -- the scenic route.'
  3. **Polynomial quotient:** 'Algebraic but less direct -- the backstage pass.'
  4. **Algebraic closure:** 'Abstract but powerful -- the mysterious wizard.'
- **Geometers:** 'A plane with a built-in rotation operator, most naturally captured by matrices.'
  1. **Matrix model:** 'The geometric favourite -- smooth moves on the dance floor.'
  2. **Ordered-pair model:** 'Concrete and visual -- the reliable partner.'
  3. **Polynomial quotient:** 'Algebraic foundation -- the sturdy shoes.'
  4. **Algebraic closure:** 'More abstract -- the enigmatic stranger.'
- **Category theorists:** 'The algebraic closure of $\mathbb{R}$. Also a $1$-dimensional complex vector space. Also a monoidal category if you squint.'
  1. **Algebraic closure:** 'Ultimate categorical object -- the VIP of fields.'
  2. **Polynomial quotient:** 'Clear algebraic construction -- the blueprint.'
  3. **Ordered-pair model:** 'Concrete but less categorical -- the casual attendee.'
  4. **Matrix model:** 'Geometric but less categorical -- the artsy outsider.'

---

## 5. The quaternions (ℍ)

We're getting to a point where it's getting harder to justify the existence of new number systems purely on structural grounds. William Rowan Hamilton attempted to extend the complex numbers to a 3-dimensional system, but found that multiplication could not be consistently defined in 3 dimensions while preserving the desired algebraic properties. Instead, he discovered a 4-dimensional system in 1843: the quaternions, a noncommutative but associative division algebra.

Later in 1877, Ferdinand Georg Frobenius showed that the quaternions are one of only 3 associative division algebras over the reals (the others being $\mathbb{R}$ and $\mathbb{C}$). This result was extended by Adolf Hurwitz, who classified normed division algebras, showing that the only normed division algebras over the reals are $\mathbb{R}$, $\mathbb{C}$, $\mathbb{H}$ and the octonions $\mathbb{O}$.

**In real life:** Quaternions are used in 3D computer graphics and robotics to represent rotations. A unit quaternion acts on 3‑dimensional space by conjugation, avoiding issues like gimbal lock that can occur with Euler angles.[^2]

[^2]: A 3D rotation by a unit quaternion $q \in S^3$ acts on a vector $v \in \operatorname{Im}(\mathbb{H}) \cong \mathbb{R}^3$ via the map $v \mapsto qvq^{-1}$. (I might write a separate post on this later.)

### ℍ: Construction

Two main approaches:

#### (5A) Free associative algebra quotient

- Start with $\mathbb{R}\langle i, j \rangle$, the free associative algebra on generators $i$ and $j$.
- Impose relations: $i^2 = j^2 = -1$, $ij = -ji$.
- Define $k = ij$.

From the relation $k = ij$, the other quaternionic multiplication rules fall out naturally, such as

$$k^2 = (ij)(ij) = i(ji)j = -i^2j^2 = -(-1)(-1) = -1$$

as well as $jk = i$, $ki = j$, and the cyclic identities. We see that $\mathbb{H}$ is noncommutative but associative.

**Equivalent presentation:** $\mathbb{H} \cong \mathbb{R}\langle i,j \rangle / (i^2 + 1, j^2 + 1, ji + ij) \cong \mathbb{C}\langle j \rangle / (j^2 + 1, ji + ij)$, where $i \in \mathbb{C}$.

This can also be phrased as a $4$-dimensional real associative algebra with basis $\{1, i, j, k\}$ and the defining relations above.

#### (5B) Cayley--Dickson doubling

Start with $\mathbb{C}$ and form $\mathbb{H}$ as $\mathbb{C}^2$ with twisted multiplication:

$$(a,b)(c,d) = (ac - d\bar{b}, \bar{a}d + cb)$$  

where $\bar{a}$ denotes complex conjugation.

This doubling process also constructs $\mathbb{C}$ from $\mathbb{R}$ by the same formula, taking $\mathbb{R}^2$ with twisted multiplication.

The Cayley--Dickson construction produces a normed division algebra, doubling dimension at each step (at the expense of losing some algebraic properties like commutativity and then associativity).

### ℍ: How mathematicians feel about it

- **Algebraists:** 'Noncommutative but associative. A respectable rebel.'
  - **Free associative algebra quotient:** 'The classic, algebraically rich construction -- like a jazz solo with rules.'
  - **Cayley--Dickson doubling:** 'Elegant and recursive -- the fractal of algebras.'
- **Analysts:** 'Unit quaternions give rotations. I like rotations.'
  - **Cayley--Dickson doubling:** 'Connects nicely to complex numbers and rotations -- smooth operator.'
  - **Free associative algebra quotient:** 'More algebraic, less intuitive -- the theory nerd.'
- **Geometers:** '$SO(3)$ in disguise.'
  - **Cayley--Dickson doubling:** 'Geometric and intuitive -- the smooth dancer.'
  - **Free associative algebra quotient:** 'Algebraic but less geometric -- the bookworm.'
- **Category theorists:** 'A monoid object in real vector spaces with a braiding that mysteriously vanishes. Strange. Intriguing. Needs more diagrams.'
  - **Free associative algebra quotient:** 'Clear algebraic presentation -- the neat freak.'
  - **Cayley--Dickson doubling:** 'Recursive but less categorical -- the recursive thinker.'

---

## 6. The octonions (𝕆)

Yeah, I'm not even going to try to justify the octonions. They exist because they do. Discovered in 1843 by John T Graves, a friend of Hamilton, they fit into the beautiful pattern of normed division algebras over the reals classified by Hurwitz. But the buck stops here: there are no further normed division algebras beyond $\mathbb{O}$.

**In real life:** The octonions only exist because the algebraic pattern demands them. There is no compelling real‑life application.

### 𝕆: Construction

Cayley--Dickson doubling applied to $\mathbb{H}$. An 8-dimensional normed division algebra.

Associativity is lost (this is genuinely a bit wild), but alternativity remains. In general, $(xy)z \neq x(yz)$ for $x,y,z \in \mathbb{O}$. Yes, this means you now have to care about brackets. No, everyone is not okay with this.

### 𝕆: How mathematicians feel about it

- **Algebraists:** 'Nonassociative? Deep breaths. At least it's alternative...'
- **Analysts:** 'The norm is multiplicative. I'm choosing to focus on that.'
- **Geometers:** '$G_2$ lives here. Exotic, beautiful and slightly unsettling.'
- **Category theorists:** 'Nonassociative? Perfect. Structure is optional anyway.'

---

## Comparative ranking (leaning into the stereotypes)

At this point, having exhausted all structural justifications, we turn to vibes. I'm going to rank the 6 number systems according to how much each mathematical tribe likes them, from most to least favourite.

### Algebraists

1. $\mathbb{Z}$ -- Construction perfection. The simplest ring, the bedrock of algebraic dreams. It's like the plain bagel of number systems: humble, essential, and infinitely versatile.
2. $\mathbb{Q}$ -- Localisation bliss. Fractions done right, the algebraist's Swiss Army knife. Elegant, canonical, and just complicated enough to feel grown-up.
3. $\mathbb{R}$ -- A completion. Very tasteful. Like adding cream cheese to the bagel: smooth, refined, and absolutely necessary for analysis.
4. $\mathbb{C}$ -- A quadratic extension. Clean. The algebraic upgrade that adds a dash of mystery and a pinch of magic.
5. $\mathbb{H}$ -- Noncommutative but still associative. The rebellious teenager of algebras: breaking some rules but still playing by most.
6. $\mathbb{O}$ -- 'I mean... fine, but why?' The wild card. Nonassociative, unsettling, but somehow still fascinating.

### Analysts

1. $\mathbb{R}$ -- The *One True Number System*. Limits, continuity and all that jazz. The warm blanket of analysis.
2. $\mathbb{C}$ -- Holomorphic functions are sorcery. The playground where magic happens and everything is beautifully smooth.
3. $\mathbb{Q}$ -- Dense and countable. Like a well-organized library, but missing the comfy chairs and the heating.
4. $\mathbb{Z}$ -- Endpoints of intervals. The rigid scaffolding that holds up the continuous world.
5. $\mathbb{H}$ -- Rotations are neat. Handy for 3D spins, but a bit too algebraic for everyday analysis.
6. $\mathbb{O}$ -- 'I refuse to think about this.' The analyst's equivalent of a stress dream.

### Geometers

1. $\mathbb{R}$ -- The line. The simplest, smoothest path.
2. $\mathbb{C}$ -- The plane. Where geometry gets its groove on.
3. $\mathbb{H}$ -- 3D rotations. The dance floor of spatial transformations.
4. $\mathbb{O}$ -- $G_2$ and exotic spheres. The mysterious guest at the geometry party who somehow knows everyone.
5. $\mathbb{Q}$ -- Rationals are too spiky. Like a cactus in a rose garden.
6. $\mathbb{Z}$ -- A sad discretisation. The grid lines that remind you geometry isn't always smooth.

### Category theorists

1. $\mathbb{Z}$ -- Initial ring. A king. The universal starting point, the ruler of all rings.
2. $\mathbb{Q}$ -- Localisation. A colimit. A dream. The construction everyone else was groping towards.
3. $\mathbb{R}$ -- Reflective subcategory of ordered fields. The sophisticated adult in the room.
4. $\mathbb{C}$ -- Algebraic closure. Terminal in spirit. The categorical VIP.
5. $\mathbb{O}$ -- Nonassociativity is a feature. Finally, something that behaves like they secretly want.
6. $\mathbb{H}$ -- 'Too associative. Needs more coherence laws.' The overachiever who just can't relax.

---

This post captures the constructions of various number systems and the personalities they attract. The number systems form a ladder of increasing algebraic chaos, and each mathematical tribe has its own favourite rung.

Thank you for reading this far. Whether you skimmed the constructions or lingered over them, I'm glad you were here. If you have a favourite construction, a different ranking, a proof you want to share or would like to see, or even a strong reaction to any of this, please share it in a comment below :)
