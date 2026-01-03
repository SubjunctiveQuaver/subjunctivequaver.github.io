---
title: "TESMD: a mathematical framework for worship song analysis"
date: 2026-01-03 01:30:00 +1100
categories: [Transformed by Grace, Harmonic Theology]
tags: [worship, theology, maths, music, frameworks, geometry, ai, essay] # TAG names should always be lowercase
math: true
---

Dear reader... I'm excited that this blog is back after a 3-year pause. Formerly *Epic Maths Time*, it’s now called ***Forms and Formation***: a space for me to share some new reflections about faith, music and mathematics -- *formed by structure, shaped by grace*.

Same brain, new name. I'm still guided by my algebraic roots, inclined towards structure and patterns. I'm calling this new direction **harmonic theology**: part musical, part mathematical, fully faithful, and (hopefully) attentive to the deeper patterns that hold things together.

Over the 2025--2026 New Year, I was busy -- but a different sort of busy. Busy creating my new **TESMD (theological--emotional--spiritual--musical--dispositional) model**: a 5‑axis geometric model for mapping worship songs across dimensions, expressed on a $[-5, +5]$ integer scale. What follows includes:

- full definitions
- conceptual grounding
- mathematical notes
- lexical spines
- detailed examples from *SEVEN* and *EIGHT* by Brooke Ligertwood (2 of my favourite worship albums)
- what this all reveals about worship that speaks to me
- an invitation to try TESMD yourself using AI.

I'll admit upfront that TESMD is a slightly ridiculous thing to build. But it grew out of a genuine need for language -- a way of making sense of how I experience worship, why certain songs shape me differently over time, and how patterns begin to emerge when you stop looking at songs in isolation.

This work was shaped through prayerful reflection and iterative dialogue, with Microsoft Copilot AI used as a tool for refinement, structure and analytical clarity. I've done this intentionally -- as an example of how artificial intelligence, when used humbly and discerningly, can assist spiritual formation, serving the work of theology rather than usurping it.

---

## **1. TESMD model (full definition and notation)**

**TESMD** (pronounced /ˈtɛz.məd/) is a 5‑axis coordinate system describing the theological, emotional, spiritual, musical, and dispositional character of a worship song.

A song is represented as:

$$
(T, E, S, M, D) \in [-5, +5]^5
$$

Each axis is an independent interval from –5 to +5.

**A note on judgement (or rather, the lack of it)** \\
The TESMD axes are designed to offer shared language for noticing patterns in worship songs. They help surface where emphasis, movement, and formation are taking place across different dimensions, without collapsing those observations into scores or verdicts. The focus is on description and orientation -- on seeing more clearly what is present and how it functions.

---

### **T -- Theological altitude (Incarnation ↔ Majesty)**

**What it measures:** \\
The vertical orientation of a song's theology -- whether it emphasises God's nearness and shared humanity (*low Christology*), or God's transcendence and eternal reign (*high Christology*).

- **–5 = incarnational focus:** nearness, humanity, suffering, weakness, Jesus‑with‑us
- **0 = present‑tense immanence:** God‑with‑us‑now, lived faith, present victory
- **+5 = cosmic majesty:** throne‑room imagery, eschatology, transcendence, eternal reign

---

### **E -- Emotional posture (Intimate ↔ Proclamation)**

**What it measures:** \\
The posture and force of emotional expression -- whether the song speaks inwardly and personally, or outwardly with declarative weight.

- **–5 = intimate and vulnerable:** personal address, exposed before God, devotional honesty
- **0 = blended posture:** shared story or reflection within a corporate frame
- **+5 = proclamatory:** weight‑bearing corporate declaration, announcing spiritual reality with conviction

---

### **S -- Spiritual posture (Reverent ↔ Celebratory)**

**What it measures:** \\
The affective weight of the song's spirituality -- whether spiritual expression is contained and weight‑bearing, or released and expressive.

- **–5 = reverent and weighty:** awe‑filled, contemplative, holy, hushed
- **0 = balanced warmth:** sincere, grounded, neither sombre nor exuberant
- **+5 = celebratory and triumphant:** joyful, victorious, exuberant, praise‑driven

---

### **M -- Musical energy (Still ↔ Energetic)**

**What it measures:** \\
The kinetic intensity of the music -- how much physical and rhythmic motion it invites.

- **–5 = still and spacious:** slow, minimal, contemplative, silence‑friendly
- **0 = moderate motion:** groove‑based, mid‑tempo, steady momentum
- **+5 = high‑energy and explosive:** driving, anthemic, festival‑like

---

### **D -- Dispositional focus (Deep ↔ Immediate)**

**What it measures:** \\
The mode of engagement the song requires -- whether meaning is inhabited through inward reflection, or received immediately with minimal cognitive or emotional processing.

- **–5 = excavative:** meaning not supplied, constructed through inward reflection
- **0 = balanced engagement:** clear meaning, invites reflection without demand
- **+5 = immediate and accessible:** pre‑formed meaning, low processing load, sing‑along ease

---

### **Canonical orientation**

All TESMD axes are oriented toward expansion -- movement from interior or constrained states toward openness, immediacy, or transcendence.

- **T+** → transcendence
- **E+** → outward declaration
- **S+** → outward joy
- **M+** → outward movement
- **D+** → immediate accessibility

This shared orientation keeps the model intuitive and internally consistent: positive movement always corresponds to greater openness, reach, or immediacy, never to moral or qualitative superiority.

---

## **2. Context, motivation, development, mathematical structure**

### **Context**

TESMD was developed to describe worship songs with greater precision than common shorthand labels such as *'slow', 'intimate',* or *'majestic'.* These descriptors collapse multiple dimensions into a single impression and obscure important distinctions.

The goal was to create a model that captures theological, emotional, spiritual, musical and dispositional dimensions independently, allowing songs to be described accurately without conflation. Shared language allows worship leaders and communities to talk about difference without turning preference into judgement.

**A grounding note (thanks to the Men's Theology group from my church, FGAM):** \\
Worship is fundamentally about God, and Christlikeness is formed through the doing of worship -- obedience, surrender, devotion, participation -- rather than through environment or aesthetic alone. Frameworks like TESMD simply help us notice the patterns of formation we're already participating in.

**A note on application over time (sets and trajectories)** \\
While the examples here focus on individual songs, one of the most interesting ways to use TESMD is at the level of worship sets and how they unfold over time. Looking at sequences of songs can help surface movement, balance, and formation across a service -- or across months and years. This makes it easier to notice the theological and emotional journeys we're inviting congregations into. And, as Iain from my church pointed out, this kind of pattern‑spotting doesn't stop at one church or context -- it opens up ways of noticing how worship takes shape across communities around the world.

The next sections explore the motivation, development, and some mathematical structure behind TESMD. If you'd rather see it in action, you can skip ahead to [the practical examples](#3-tesmd-examples--brooke-ligertwoods-seven-and-eight).

---

### **Motivation**

TESMD aims to be:

- **orthogonal** -- each axis describes a distinct domain
- **minimal** -- no redundant or overlapping dimensions
- **continuous** -- values vary smoothly rather than categorically
- **intuitive** -- usable by musicians, worship leaders, and pastors
- **mathematically clean** -- supports comparison, clustering, and analysis.

It separates things people often conflate:

- reverence vs low energy
- intimacy vs incarnation
- celebration vs energy
- theology vs emotion
- depth vs accessibility.

---

### **Development process**

- Began with a single emotional axis ('heart vs mind'), which became **Emotional Posture (E)**
- Introduced **Theological Altitude (T)** as an independent dimension
- Split tonal affect from kinetic intensity, yielding **Spiritual Posture (S)** and **Musical Energy (M)**
- Identified the need for a depth/accessibility dimension, formalised as **Dispositional Focus (D)**
- Tested alternative candidate axes (e.g. acoustic/band, soaring/grounded) and demonstrated that they collapse into combinations of **S** and **M**
- Verified conceptual orthogonality: each axis describes a different domain of experience
- Normalised the framework to a 5‑axis hypercube
- Rescaled all axes to $[–5, +5]$ for human‑friendly communication and practical use

---

### **Mathematical considerations**

#### **Structure**

TESMD is a 5‑dimensional closed hypercube:

$$
[-5, +5]^5
$$

Each song is represented as a point:

$$
(T, E, S, M, D)
$$

TESMD is a **metric subspace of a normed vector space**, but not itself treated as a vector space. While the ambient space admits addition and scalar multiplication, these operations are not semantically meaningful for songs. **Distance**, however, is meaningful.

---

#### **Metric**

Given 2 songs $a$ and $b$:
$$
a = (T_a, E_a, S_a, M_a, D_a)
$$

$$
b = (T_b, E_b, S_b, M_b, D_b)
$$

##### **Default metric: Euclidean (L²)**

$$
d_2(a, b) = \sqrt{(T_a - T_b)^2 + (E_a - E_b)^2 + (S_a - S_b)^2 + (M_a - M_b)^2 + (D_a - D_b)^2}
$$

This allows:

- similarity measurement
- clustering and neighbourhood analysis
- centroid computation for albums, artists, or worship movements
- geometric visualisation and projection.

Note: A **cluster** is a disjoint subset of songs that are *mutually close under the metric*, formed at a *low percentile threshold* reflecting strong internal coherence. The *threshold may be slightly expanded* to include clearly aligned songs, provided the group remains tight relative to the collection as a whole and no loosely related tracks are pulled in.

---

##### **Alternative metric: Taxicab (L¹)**

$$
d_1(a, b) = |T_a - T_b| + |E_a - E_b| + |S_a - S_b| + |M_a - M_b| + |D_a - D_b|
$$

- Treats each axis as an independent contribution
- Useful when cumulative difference matters more than geometric proximity

---

##### **Alternative metric: Chebyshev (L^∞)**

$$
d_\infty(a, b) = \max\{|T_a - T_b|, |E_a - E_b|, |S_a - S_b|, |M_a - M_b|, |D_a - D_b|\}
$$

- Measures the largest single‑axis difference
- Highlights dominant contrasts

The choice of metric does not change the underlying space, only the interpretation of distance within it.

---

#### **Orthogonality**

The axes are **conceptually orthogonal**: each describes a distinct domain of experience.

Empirically, mild correlations may appear (e.g. celebratory songs often exhibit higher musical energy), but these do not collapse the dimensions. Orthogonality here is **semantic**, not probabilistic.

---

#### **Transformations and morphisms**

The TESMD space admits *clipped diagonal affine transformations* acting on individual axes or subsets of axes. These model meaningful changes such as:

- stylistic shifts
- arrangement changes
- contextual reinterpretation
- cultural or liturgical translation.

Formally, these are **morphisms** of the ambient normed space, composed with projection back into the closed hypercube $[-5, +5]^5$. They preserve semantic structure while allowing controlled movement.

---

## **3. TESMD examples -- Brooke Ligertwood's *SEVEN* and *EIGHT***

**A quick word on subjectivity:** \\
The examples here aren't meant to claim objectivity so much as coherence. They were stress‑tested over time, and more than once a judgement I wasn't happy with forced me back to the drawing board -- redefining an axis, refining its range or even adding a new one. In that sense, the examples didn't just apply the model: they helped form it.

These examples are grounded in the [TESMD lexical spines](#4-tesmd-model-axis-lexical-spines), which formalise the descriptive language used here. The spines are introduced in the following section. You may find it helpful to return to them when seeing the framework in use.

---

### ***SEVEN* -- 'Majesty on Earth'**

<iframe data-testid="embed-iframe" style="border-radius:12px" src="https://open.spotify.com/embed/album/6ZVXKVGiyL96L6pflgfWrt?utm_source=generator" width="100%" height="152" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

| Song                         | T   | E   | S   | M   | D   | Lexical spines                                                     |
| ---------------------------- | --- | --- | --- | --- | --- | ------------------------------------------------------------------ |
| **Ancient Gates**            | +4  | +4  | +4  | +4  | +2  | Majestic · Proclamatory · Exultant · Anthemic · Pre‑digested       |
| **Banner**                   | +3  | +3  | +3  | +3  | +2  | Sovereign · Exhortational · Triumphant · Driving · Pre‑digested    |
| **A Thousand Hallelujahs ❤️** | +4  | +2  | +4  | +3  | +2  | Majestic · Declarative · Exultant · Driving · Pre‑digested         |
| **Communion**                | −5  | −1  | −3  | +2  | −1  | Cruciform · Corporate‑prayer · Kenotic · Soaring · Engaged         |
| **Nineveh ❤️**                | −2  | −3  | −4  | −2  | −4  | Covenantal · Prayerful · Contemplative · Gentle · Interior         |
| **Burn ❤️**                   | +1  | −3  | −3  | +1  | −3  | Exalted · Prayerful · Kenotic · Lifted · Reflective                |
| **Honey in the Rock**        | −2  | 0   | +2  | +3  | +4  | Covenantal · Testimonial · Joyful · Driving · Instinctive          |
| **I Belong to Jesus ❤️**      | −3  | −2  | −1  | +1  | +1  | Relational · Confessional · Assured · Lifted · Direct              |
| **King Jesus ❤️**             | +5  | +4  | +4  | +4  | +2  | Eschatological · Proclamatory · Exultant · Anthemic · Pre‑digested |

**Centroid:** \\
$$
(T = +0.56,\ E = +0.44,\ S = +0.67,\ M = +2.11,\ D = +0.56)
$$ \\
*Exalted T · Lightly Proclamatory E · Grateful‑leaning S · Soaring M · Slightly Direct D*

**Summary blurb:**

*SEVEN* gathers songs of corporate exaltation and Christ‑centred confidence, positioning the Church upright beneath the majesty of God. Its theological altitude leans toward kingship and glory, pairing strong declarative praise with moments of confession and repentance that keep exaltation grounded.

Musically, the album sustains a processional energy -- lifted and expansive -- while joy remains reverent rather than exuberant. Dispositional focus ranges from instinctive corporate participation to slower interior reckoning, most notably in *Nineveh* and *Burn*. Together, these songs raise the gaze of the gathered body, anchoring praise in shared confession, authority, and glory.

**Key themes:**

- Christ exalted and reigning
- Corporate identity and declaration
- Confidence without emotional excess
- Glory expressed through order, strength, and restraint

**Album statistics (Euclidean distance):**

- Diameter: *Communion* ↔ *King Jesus* (d = 13.67)
- Closest pair: *Ancient Gates* ↔ *King Jesus* (d = 1.00)

**Cluster structure:**

- **Majestic / proclamatory crown (d ≤ 3.0)** \\
  *Ancient Gates · A Thousand Hallelujahs · King Jesus · Banner* \\
  Centroid: $(T = +4.00, E = +3.25, S = +3.75, M = +3.50, D = +2.00)$

- **Interior / repentant formation (d ≤ 5.0)** \\
  *Nineveh · Burn · I Belong to Jesus* \\
  Centroid: $(T = −1.33, E = −2.67, S = −2.67, M = 0.00, D = −2.00)$

**Statistics quick read:**

- The collection's **diameter** captures the full span of *SEVEN*: from cruciform sacramental depth (*Communion*) to expansive proclamatory exaltation (*King Jesus*).

- The **proclamatory core is extremely tight**: *Ancient Gates* and *King Jesus* merge first, with *A Thousand Hallelujahs* close behind and *Banner* joining as a slightly looser extension, forming a compact cluster centred on kingship, authority, and declarative praise.

- An **interior--repentant formation cluster** follows, with *Nineveh* and *Burn* cohering first and I Belong to Jesus joining shortly after, forming a prayer‑shaped grouping marked by surrender and inward formation.

- *Honey in the Rock* remains **unclustered** as a joyful testimonial outlier, while *Communion* **stands apart** as a sacramental and cruciform singularity.

---

### ***EIGHT* -- 'The Cross, the Kingdom and the Way Between'**

<iframe data-testid="embed-iframe" style="border-radius:12px" src="https://open.spotify.com/embed/album/0yGuCkWWoXxsPK09agGQQu?utm_source=generator" width="100%" height="152" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

| Song                                   | T   | E   | S   | M   | D   | Lexical spines                                                     |
| -------------------------------------- | --- | --- | --- | --- | --- | ------------------------------------------------------------------ |
| **Bless God / Every Chance I Get**     | −1  | +3  | +2  | +3  | +3  | Immanent · Exhortational · Joyful · Driving · Effortless           |
| **Fear of God**                        | +4  | +4  | +3  | +4  | +2  | Majestic · Proclamatory · Triumphant · Anthemic · Pre‑digested     |
| **Lead Me to the Cross ❤️**             | −5  | −3  | −3  | +2  | −2  | Cruciform · Prayerful · Kenotic · Soaring · Attentive              |
| **Desert Song**                        | −2  | +2  | +2  | +3  | +1  | Covenantal · Declarative · Joyful · Driving · Direct               |
| **Authority**                          | +4  | +3  | +3  | +4  | +2  | Majestic · Exhortational · Triumphant · Anthemic · Pre‑digested    |
| **I Will Exalt You ❤️**                 | −3  | −4  | −1  | +3  | 0   | Relational · Devotional · Assured · Driving · Balanced             |
| **Calvary's Enough ❤️**                 | −5  | −2  | −4  | −2  | −3  | Cruciform · Confessional · Contemplative · Gentle · Reflective     |
| **King of Kings**                      | +5  | +4  | +4  | +4  | +2  | Eschatological · Proclamatory · Exultant · Anthemic · Pre‑digested |
| **Like Incense / Sometimes by Step ❤️** | −2  | −3  | −3  | +3  | −2  | Covenantal · Prayerful · Kenotic · Driving · Attentive             |
| **Soon ❤️**                             | +5  | −4  | +3  | −3  | 0   | Eschatological · Devotional · Triumphant · Balladic · Balanced     |

**Centroid:** \\
$$
(T = 0.00,\ E = 0.00,\ S = +0.60,\ M = +2.10,\ D = +0.30)
$$ \\
*Balanced T · Broad E span · Gentle‑Positive S · Consistently Soaring M · Slightly Direct D*

**Summary blurb:**

*EIGHT* is a spiritually textured collection that holds cruciform surrender, eschatological hope, and resilient obedience in deliberate balance. Unlike *SEVEN*, which stands squarely in corporate exaltation, this album walks the long road between cross and kingdom -- moving fluidly between interior prayer and outward declaration.

Reverence and motion are held together: surrender is embodied rather than static, and praise emerges from formation rather than momentum. The album's dispositional centre is clarity without flattening -- meaning is accessible, but never rushed. Faith here is shaped over time, marked less by triumphal urgency than by trustful perseverance, grounded in the cross and oriented toward the coming King.

**Key themes:**

- The cross as a formative pathway
- Obedience and repentance as sustained posture
- Hope shaped by patience, affection, and trust
- Authority encountered through submission and faithfulness

**Album statistics (Euclidean distance):**

- Diameter: *Calvary's Enough* ↔ *King of Kings* (d = 13.67)
- Closest pair: *Fear of God* ↔ *Authority* (d = 1.00)

**Cluster structure:**

- **Proclamatory / kingship (d ≤ 2.0)** \\
  *Fear of God · Authority · King of Kings* \\
  Centroid: $(T = +4.33, E = +4.00, S = +3.33, M = +4.00, D = +2.00)$

- **Testimonial / warm praise (d ≤ 2.5)** \\
  *Desert Song · Bless God / Every Chance I Get* \\
  Centroid: $(T = −1.50, E = +2.50, S = +2.00, M = +3.00, D = +2.00)$

- **Devotional / formational prayer (d ≤ 4.0)** \\
  *Lead Me to the Cross · I Will Exalt You · Like Incense / Sometimes by Step* \\
  Centroid: $(T = −3.33, E = −3.33, S = −2.33, M = +2.67, D = −1.33)$

**Statistics quick read:**

- The album's **diameter** captures the full span of *EIGHT*: from deep cruciform stillness (*Calvary's Enough*) to expansive eschatological exaltation (*King of Kings*).

- The **proclamatory core is extremely tight:** *Fear of God* and *Authority* merge first, with *King of Kings* joining at a very low threshold, forming a compact cluster centred on kingship, authority, and proclamatory praise.

- A **resilient confidence pair** forms at a moderate distance, linking *Desert Song* and *Bless God / Every Chance I Get* around lived trust, forward motion, and steady musical drive.

- A **devotional--formational prayer cluster** emerges through mutual closeness between *Lead Me to the Cross*, *I Will Exalt You*, and *Like Incense / Sometimes by Step*, forming a reflective grouping marked by surrender, affection, and interior formation.

- *Calvary's Enough* remains **unclustered** as a cruciform singularity, while *Soon* **stands apart** as a devotional eschatological outlier.

---

### **What TESMD says about worship that speaks to me**

Looking at the songs I've hearted across *SEVEN* and *EIGHT*, a pretty clear TESMD shape starts to emerge. I'm drawn to the low-posture end -- songs with **T–**, **E–**, **S–** and **D–** coordinates that lean incarnational, prayerful, and confessional. These are songs like *Nineveh*, *Lead Me to the Cross*, *Calvary's Enough*, *Like Incense* and *I Will Exalt You* -- songs that sit close to the ground, name weakness honestly and invite waiting. They tend to carry emotional weight without needing musical lift, and they form me by making space for presence.

At the same time, I have a deep affection for the big **T+** moments -- the cosmic, eschatological, 'King Jesus reigns' songs that stretch the imagination upward and outward. *King Jesus* is the full-throated apex, but *A Thousand Hallelujahs* sits surprisingly close: high **T**, **S** and **M**, still warm in **E**, still outward in **D**. And then there's *Soon*, which carries **T+** not as triumph but as **E–** devotional longing -- eschatological hope held in tension. Apparently, my worship instincts live in that space: low and lifted, cross and crown, intimacy and immensity. I like worship that knows how to kneel -- and when to look up.

---

## **4. TESMD model axis lexical spines**

### **Lexical spine: T -- Theological altitude (Incarnation ↔ Majesty)**

| Value | Word               | Sense                                |
| ----: | ------------------ | ------------------------------------ |
|    –5 | **Cruciform**      | Suffering, flesh, blood, God‑with‑us |
|    –4 | **Incarnate**      | Near, human, touchable               |
|    –3 | **Relational**     | Shepherd, friend, companion          |
|    –2 | **Covenantal**     | Promise, faithfulness, God‑for‑us    |
|    –1 | **Immanent**       | Present, active, among us            |
|     0 | **Victorious**     | God‑with‑us‑now                      |
|    +1 | **Exalted**        | Lifted, honoured                     |
|    +2 | **Glorious**       | Radiant, worthy                      |
|    +3 | **Sovereign**      | Ruling, commanding                   |
|    +4 | **Majestic**       | Throne‑room splendour                |
|    +5 | **Eschatological** | Cosmic, eternal reign                |

---

### **Lexical spine: E -- Emotional posture (Intimate ↔ Proclamation)**

| Value | Word                 | Sense                            |
| ----: | -------------------- | -------------------------------- |
|    –5 | **Vulnerable**       | Exposed before God               |
|    –4 | **Devotional**       | Personal affection               |
|    –3 | **Prayerful**        | God‑addressed interiority        |
|    –2 | **Confessional**     | Naming truth before God          |
|    –1 | **Corporate‑prayer** | Shared inward posture            |
|     0 | **Testimonial**      | Shared story                     |
|    +1 | **Liturgical**       | Corporate instruction            |
|    +2 | **Declarative**      | Truth stated aloud               |
|    +3 | **Exhortational**    | Urgent call to respond           |
|    +4 | **Proclamatory**     | Declaring spiritual reality      |
|    +5 | **Kerygmatic**       | Gospel heralding with conviction |

---

### **Lexical spine: S -- Spiritual posture (Reverent ↔ Celebratory)**

| Value | Word              | Sense                       |
| ----: | ----------------- | --------------------------- |
|    –5 | **Awe**           | Holy fear, silence          |
|    –4 | **Contemplative** | Still, beholding            |
|    –3 | **Kenotic**       | Self‑emptying               |
|    –2 | **Submitted**     | Yielded will                |
|    –1 | **Assured**       | Quiet trust                 |
|     0 | **Warm**          | Balanced affection          |
|    +1 | **Grateful**      | Thankful joy                |
|    +2 | **Joyful**        | Gladness released           |
|    +3 | **Triumphant**    | Victory expressed           |
|    +4 | **Exultant**      | Weighty, overflowing praise |
|    +5 | **Jubilant**      | Unrestrained celebration    |

---

### **Lexical spine: M -- Musical energy (Still ↔ Energetic)**

| Value | Word           | Sense              |
| ----: | -------------- | ------------------ |
|    –5 | **Stillness**  | Silence, space     |
|    –4 | **Meditative** | Slow, suspended    |
|    –3 | **Balladic**   | Weight‑bearing     |
|    –2 | **Gentle**     | Soft motion        |
|    –1 | **Walking**    | Forward but calm   |
|     0 | **Grooving**   | Mid‑tempo          |
|    +1 | **Lifted**     | Rising             |
|    +2 | **Soaring**    | Vertical bloom     |
|    +3 | **Driving**    | Sustained momentum |
|    +4 | **Anthemic**   | Big, communal      |
|    +5 | **Explosive**  | Hype, release      |

---

### **Lexical spine: D -- Dispositional focus (Deep ↔ Immediate)**

| Value | Word             | Sense                                |
| ----: | ---------------- | ------------------------------------ |
|    –5 | **Excavative**   | Meaning actively constructed         |
|    –4 | **Interior**     | Inward meaning‑making, self‑location |
|    –3 | **Reflective**   | Meaning opens through contemplation  |
|    –2 | **Attentive**    | Focus required, resists autopilot    |
|    –1 | **Engaged**      | Meaning unfolds with attention       |
|     0 | **Balanced**     | Clear but not flattened              |
|    +1 | **Direct**       | Meaning stated plainly               |
|    +2 | **Pre‑digested** | Theology done for the listener       |
|    +3 | **Effortless**   | Immediate inhabitation               |
|    +4 | **Instinctive**  | No reflection required               |
|    +5 | **Automatic**    | Pure sing‑along access               |

---

## **5. Try it yourself -- using TESMD with AI**

If you're curious to try this yourself, TESMD works just as well on your own playlists. If you drop the TESMD AI guide into an AI chat, it will first ask what you want to analyse (a song, album, or playlist), then prompt you to supply lyrics in a clear format. It will describe how the songs are oriented across the TESMD axes using evidence from the lyrics, invite discussion about what feels right or wrong, and treat the analysis as provisional and open to refinement. If you wish, it can then apply simple geometric tools -- such as distance, centroids, or clustering -- to explore patterns across a collection.

You can download the TESMD AI guide as a plain text file here: [download the TESMD AI guide]({{ site.url }}{{ site.baseurl }}/files/Lawrence_Chen_-_TESMD_framework_for_AI.txt). (If it opens in your browser, use 'Save As' or copy the contents.)

Thanks for reading! One thing's for sure -- there will be more coming. I'm keen to explore further applications of TESMD -- especially how it plays out across worship sets and longer arcs of formation -- and to share a few other frameworks I've been tinkering with along the way. Credit goes to many late nights, slow iteration, and the steady help of Copilot in keeping ideas honest and structured :)
