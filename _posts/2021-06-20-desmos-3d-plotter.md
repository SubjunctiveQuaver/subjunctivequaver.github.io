---
title: An interactive visualisation of immersed surfaces on Desmos
date: 2021-06-20 00:40:00 +1000
categories: [Epic Maths Time, Cool Stuff]
tags: [differential-geometry, linear-algebra, uni-maths] # TAG names should always be lowercase
math: true
---

Note: this article is currently a WIP.

## Some examples of surface visualisations

Here are a couple of versions of the Desmos save file with different cool pre-loaded plots:

- The default: [a hemisphere (select the second plot for a full sphere)](https://www.desmos.com/calculator/u5ma8mrq4e)
- [A mobius band](https://www.desmos.com/calculator/dqsysshxwj)
- [A heliocoid](https://www.desmos.com/calculator/p3ztoufvpn)
- [An immersed Klein bottle in $$\mathbb R^3$$](https://www.desmos.com/calculator/bdrerelimf) (thanks to cFOURbon for entering the formula)
- [A heart-shaped surface](https://www.desmos.com/calculator/fguyjsvplw)
- [A shell](https://www.desmos.com/calculator/8fth0oldky) (thanks to Kevin D. for the help and idea)

_Note: The below was submitted as my essay for the final assignment in the unit MTH3110 - differential geometry, at Monash University, in Semester 1, 2021. I've chosen to upload it here for those who may have seen my Desmos surface visualisation, and are interested in how I derived it! However, it assumes familiarity, especially near the end, with differential-geometric quantities such as maps of surfaces and their derivatives, and tangent spaces._

## The explanation and geometry of the Desmos visualisation

Here is an [interactive visualisation of surfaces](https://www.desmos.com/calculator/u5ma8mrq4e) on Desmos (a graphing website), made by me. It takes a (continuous) function $$f : U \to \mathbb R$$, for some $$U \subseteq \mathbb R^2$$, and plots a projection of the graph of $$f$$ onto $$\mathbb R^2$$ as a "wire-frame"; it can also take a parametrisation $$\sigma : U \to \mathbb R^3$$ and plot a projection of its image in the plane.[^1] We discuss the algebra and geometry used in its construction, and some geometric properties of the projection map. Henceforth, let us assume that $$U$$ is open, $$f$$ is a smooth function, and that $$\sigma$$ is a regular surface patch.

[^1]: To switch modes, click on the "plot" folder to hide it, and click on the "parametric plot" folder to show that.

### Projecting down to a plane

There are many ways to project $$\mathbb R^3$$, onto $$\mathbb R^2$$. However, a way to choose a sensible, well-behaved projection is to choose a plane $$\Pi$$ through the origin (a linear subspace of $$\mathbb R^3$$), and perform an orthogonal projection $$\pi'$$. Such a plane can be uniquely determined by using _spherical coordinates_. Consider an "observer" at $$N \in S^2$$, the unit sphere, and a standard map $$\tau : \mathbb R^2 \to S^2$$ given by

$$\tau(u,v) = (\cos u\cos v,\cos u\sin v,\sin u);$$

here, $$(u,v)$$ respectively measure latitude and longitude.[^2] The unit vectors in $$T_0\mathbb R^3$$ (denoting possible directions from the origin) are precisely points on $$S^2$$. Thus, we may take $$\Pi$$ as the orthogonal complement of the span of $$\{N\}$$.

[^2]: See Example 2.17 from MTH3110 chapter 5 notes.

A fact from differential geometry is that $$T_N S^2 = \{v \in \mathbb R^3 : N \cdot v = 0\}$$. If $$v \in \Pi$$, then for any $$kN \in \operatorname{span}\{N\}$$ (where $$k \in \mathbb R$$), $$(kN) \cdot v = k(N \cdot v) = 0$$. In particular, $$N \cdot v = 0$$, so $$v \in T_NS^2$$. Conversely, a vector $$v \in T_NS^2$$ satisfies $$(kN) \cdot v = k(N \cdot v) = 0$$ for all $$k \in \mathbb R$$, so $$v \in \Pi$$. This means that $$\Pi = T_NS^2$$, and $$N$$ is normal to this tangent space.

Next, we consider the problem of projecting from $$\mathbb R^3$$ into $$\Pi$$ (and then into $$\mathbb R^2$$). Given an orthonormal basis $$b = \{b_1,b_2\}$$ for $$\Pi$$ that extends to a right-handed orthonormal basis $$b' = \{b_1,b_2,N\}$$ of $$\mathbb R^3$$, where $$N = b_1 \times b_2$$, consider the orthogonal projection $$\pi' : \mathbb R^3 \to \Pi$$. Since $$\ker\pi' = \Pi^\perp$$ and $$\pi\vert_\Pi$$ is the identity, it follows that $$\pi'(b_1) = b_1$$, $$\pi'(b_2) = b_2$$, and $$\pi'(N) = 0$$. The map $$\pi'$$ is linear, so its matrix with respect to the bases $$b',b$$ is

$$
\pi'_{b',b} =
\begin{pmatrix}
    1 & 0 & 0 \\
    0 & 1 & 0
\end{pmatrix}.
$$

The geometry of this map is as follows: take a point $$p \in \mathbb R^3$$. Then the coset $$p + \Pi^\perp = \{p + kN : k \in \mathbb R\}$$, a line parallel to $$N$$ (thus orthogonal to $$\Pi$$) passing through $$p$$, is collapsed onto a point $$\pi'(p) \in \Pi$$; distinct parallel lines are collapsed to distinct points. This is an orthographic projection, where the axes are _not foreshortened_, that is, no length distortion due to perspective (see Figure~\mathbb Ref{fig:cylinder_perspective}).\footnote{See explanation of perspective and [foreshortening in art](https://drawpaintacademy.com/foreshortening/).} Under this projection, we consider $$\mathbb R^3$$ as the quotient $$\mathbb R^3/\Pi^\perp$$, and cannot distinguish between points on the same line parallel to $$\Pi^\perp$$; the map has rank $$2$$ and nullity $$1$$.

\begin{figure}[p!]
\centering
\includegraphics[width=0.75\textwidth]{cylinder*perspective.png}
\caption{Plot of cylinder $$\sigma : (0,2\pi) \times (-4,4) \to S$$, $$\sigma(u,v) = (v,\cos u,\sin v)$$ with perspective $$(\theta,\phi) = (0.1,-0.1)$$, using the Desmos visualisation. Observe that there is no distortion due to perspective (i.e. \_foreshortening*) in the negative $$x$$-direction.}
\label{fig:cylinder_perspective}
\end{figure}

Next, we consider the map that transforms points on $$\Pi$$ into points in $$\mathbb R^2$$. Given our basis $$b$$ for $$\Pi$$, there is a natural sense in which $$b_1$$ can be thought of as pointing "right", and $$b_2$$ as pointing "up". This is described by $$T : \Pi \to \mathbb R^2$$, the linear isometry such that $$T(b_1) = e_1$$ and $$T(b_2) = e_2$$. Letting $$e' = \{e_1,e_2\} \subseteq \mathbb R^2$$, $$T$$ is simply the identity in coordinates $$b,e'$$: $$T_{b,e'} = I_2$$, the $$2 \times 2$$ identity matrix.

Thus, our overall projection $$\pi : \mathbb R^3 \to \mathbb R^2$$ in the direction of $$\Pi$$ would be given by $$\pi = T \circ \pi'$$, with matrix $$T_{b,e'} \pi'_{b',b}$$. However, we wish to express the matrix for $$\pi$$ with respect to the standard basis $$e = \{e_1,e_2,e_3\}$$ for $$\mathbb R^3$$. For this, we recall that the _change-of-basis matrix_ from $$b'$$ to $$e$$ is given by

$$
M_{b' \to e} =
\begin{pmatrix}
    \vert & \vert & \vert \\
    b_1 & b_2 & N \\
    \vert & \vert & \vert
\end{pmatrix}.
$$

Since $$b'$$ is an orthonormal set, it follows that $$M_{b' \to e} \in O(3)$$, so $$M_{e \to b'} = (M_{b' \to e})^{-1} = (M_{b' \to e})^\top$$. It follows that the matrix for $$\pi$$ w.r.t. the bases $$e,e'$$ of $$\mathbb R^3,\mathbb R^2$$ respectively is

$$
\pi_{e,e'} = T_{b,e'} \pi'_{b',b} M_{e \to b'} =
\begin{pmatrix}
    1 & 0 \\
    0 & 1
\end{pmatrix}
\begin{pmatrix}
    1 & 0 & 0 \\
    0 & 1 & 0
\end{pmatrix}
\begin{pmatrix}
    \text{---} & b_1 & \text{---} \\
    \text{---} & b_2 & \text{---} \\
    \text{---} & N & \text{---}
\end{pmatrix} =
\begin{pmatrix}
    \text{---} & b_1 & \text{---} \\
    \text{---} & b_2 & \text{---}
\end{pmatrix} =: M.
$$

Now, recall that there is a pair $$(\theta,\phi)$$ corresponding to $$N = \tau(\theta,\phi)$$. For simplicity, we will assume that $$\theta \in (-\pi/2,\pi/2)$$, so that a suitable restriction of $$\tau$$ forms a regular chart for $$S^2$$. We aim to find an orthonormal basis for $$\Pi$$ by finding an orthonormal basis for $$T_NS^2$$. Note that $$\{\tau_u,\tau_v\}$$ forms a basis for $$T_NS^2$$, where

$$\tau_u(\theta,\phi) = (-\sin\theta\cos\phi,-\sin\theta\sin\phi,\cos\theta)$$

and

$$\tau_v(\theta,\phi) = (-\cos\theta\sin\phi,\cos\theta\cos\phi,0).$$

It is easy to check that these are orthogonal, so an orthonormal basis $$\{b_1,b_2\}$$ for $$\Pi$$ is found by normalising these vectors, yielding

$$b_2 = (-\sin\theta\cos\phi,-\sin\theta\sin\phi,\cos\theta)$$

and

$$b_1 = (-\sin\phi,\cos\phi,0).$$

(It turns out that this also works when $$\theta \in \{\pm\pi/2\}$$; these span the tangent planes $$T_{(0,0,\pm 1)}S^2 = \mathbb R^2 \times \{0\}$$!) Note that we needed to take $$b_1 = \tau_v/\lVert \tau_v\rVert$$ and $$b_2 = \tau_u/\lVert \tau_u\rVert$$, so that indeed $$b_1 \times b_2 = N = \tau(\theta,\phi)$$.

In summary, for our perspective given by spherical coordinates $$(\theta,\phi)$$ (or equivalently $$N = \tau(\theta,\phi) \in S^2$$), the projection $$\pi : \mathbb R^3 \to \mathbb R^2$$ is given by

$$
\begin{equation*}
    \pi(x,y,z) = \underbrace{
    \begin{pmatrix}
        -\sin\phi & \cos\phi & 0 \\
        -\sin\theta\cos\phi & -\sin\theta\sin\phi & \cos\theta
    \end{pmatrix}}_{M = M(\theta,\phi)}
    \begin{pmatrix}
        x \\
        y \\
        z
    \end{pmatrix} =
    \begin{pmatrix}
        -x\sin\phi + y\cos\phi \\
        -x\sin\theta\cos\phi - y\sin\theta\sin\phi + z\cos\theta
    \end{pmatrix}. \tag{*}
\end{equation*}
$$

### Visualising the surface in Desmos

If we wish to plot $$S$$ as the graph of $$f$$, take $$\sigma(u,v) = (u,v,f(u,v))$$. Then it reduces to the problem of plotting the image of $$\sigma$$, or at least its projection under $$\pi$$. It would be useless (given limitations on Desmos) to present a filled-in outline---we would get a single splotch of colour (with jagged edges)! Instead, we use the idea that the domain $$U$$ is an open subset of $$\mathbb R^2,$$\footnote{Desmos does not like strict inequalities, so they are often closed subsets instead, but we can ignore the boundary of $$U$$.} and for fixed $$(u,v) \in U$$, we consider the curves $$x_u,y_v : I_u,J_v \to U$$ in $$U$$ (for suitable open intervals $$I_u,J_v$$), where $$x_u(t) = (u,t)$$ and $$y_v(t) = (t,v)$$, i.e. we fix the $$u$$ or $$v$$ coordinate, and let the other vary.

Consider a set of points $$\{(u_i,v_i)\}_i \subseteq U$$, and the families of curves $$\{x_{u_i}\}_i,\{y_{v_i}\}_i$$ so-defined. Then for each of the curves (generically called $$\alpha : I \to U$$), we plot the image of $$\gamma = \sigma \circ \alpha : I \to S$$, a curve in $$S$$, under the projection $$\pi$$, yielding two families $$\{\pi \circ \sigma \circ x_{u_i}\}_i$$ (fixing $$(x =)\, u = u_i$$, plotted in red) and $$\{\pi \circ \sigma \circ y_{v_i}\}_i$$ (fixing $$(y =)\, v = v_i$$, plotted in blue) of curves in $$\mathbb R^2$$, representing moving along $$S$$ using $$\sigma$$, with one input fixed. In the visualisation, we assume that $$U = (a_1,a_2) \times (b_1,b_2)$$ is a box,\footnote{Technically $$U = [a_1,a_2] \times [b_1,b_2]$$, so we have a surface with boundary... but we can ignore this, as mentioned earlier.} and take $$n_1,n_2$$ curves of constant separation in $$U$$ in each direction. This creates the desired projection of the "wire-frame" on $$S$$, and varying $$(\theta,\phi)$$ allows us to visualise the plot of $$S$$ from all angles, giving it a 3-dimensional effect.

<!--- A nice fact about these curves is that each $$\alpha$$ is unit speed (in $$U$$). For $$x_{u_0} = (u,v)$$, $$\dot u = 0$$ and $$\dot v = 1$$, so $$\sigma \circ x_{u_0}$$ (in $$S$$) has speed $$\sqrt{E\dot u^2 + 2F\dot u\dot v + G\dot v^2} = \sqrt{G(u_0,t)}$$ at time $$t$$; similarly, $$\sigma \circ y_{v_0}$$ has speed $$\sqrt{E(t,v_0)}$$, where $$E,F,G$$ are the coefficients of the Riemannian metric of $$S$$;\footnote{See page 12 of MTH3110 chapter 8 notes.} hence, they are not necessarily unit speed in $$S$$. --->

### Differential geometry of the projection: changing perspective

For spherical coordinates $$(\theta,\phi)$$, let _principal latitude_ denote $$\theta_0 \in [-\pi/2,\pi/2]$$ such that there is $$\phi_0 \in \mathbb R$$ with $$\tau(\theta,\phi) = \tau(\theta_0,\phi_0)$$. We see that $$M(\theta,\phi)$$ is a smooth function of $$\theta,\phi$$, so the matrix (and projection) smoothly varies with $$\theta,\phi$$:

$$
M_\theta(\theta,\phi) =
\begin{pmatrix}
    0 & 0 & 0 \\
    -\cos\theta\cos\phi & -\cos\theta\sin\phi & -\sin\theta
\end{pmatrix}
$$

and

$$
\begin{equation*}
    M_\phi(\theta,\phi) =
    \begin{pmatrix}
        -\cos\phi & -\sin\phi & 0 \\
        \sin\theta\sin\phi & -\sin\theta\cos\phi & 0
    \end{pmatrix} \tag*{(from (*)).}
\end{equation*}
$$

Fixing a point $$p = (x,y,z) \in \mathbb R^3$$, we can think of $$\pi$$ as a function $$\mathbb R^2 \to \mathbb R^2$$, where the inputs are spherical coordinates $$(\theta,\phi)$$; let us call this map $$\pi' : \mathbb R^2 \to \mathbb R^2$$, $$(\theta,\phi) \mapsto \pi(p) = M(\theta,\phi)p$$. Then the directional derivatives of $$\pi'$$ are given by $$D_{(\theta,\phi)}\pi' : T_{(\theta,\phi)}\mathbb R^2 \to T_{\pi'(\theta,\phi)}\mathbb R^2$$, which is such that

$$
(\lambda,\mu) \mapsto \underbrace{
\begin{pmatrix}
    \vert & \vert \\
    \pi'_\theta & \pi'_\phi \\
    \vert & \vert
\end{pmatrix}}_{D\pi'(\theta,\phi)}
\begin{pmatrix}
    \lambda \\
    \mu
\end{pmatrix} =
\begin{pmatrix}
    0 & -x\cos\phi - y\sin\phi \\
    -x\cos\theta\cos\phi - y\cos\theta\sin\phi - z\sin\theta & x\sin\theta\sin\phi - y\sin\theta\cos\phi
\end{pmatrix}
\begin{pmatrix}
    \lambda \\
    \mu
\end{pmatrix}.
$$

So, if we change perspective from $$(\theta,\phi)$$ with velocity $$(\lambda,\mu) \in T_{(\theta,\phi)}\mathbb R^2$$ (i.e. increasing latitude by $$\lambda$$ and longitude by $$\mu$$), the image of $$p$$ in $$\mathbb R^2$$ moves with velocity $$D_{(\theta,\phi)}\pi'(\lambda,\mu)$$, given explicitly above. Note that

$$D_{(\theta,\phi)}\pi'(\lambda,\mu) = \lambda M_\theta(\theta,\phi)p + \mu M_\phi(\theta,\phi)p;$$

this relates the directional derivatives of $$\pi'$$ to the partial derivatives of $$M$$.

Let us consider what happens to $$\pi(p)$$ when we fix longitude $$\phi$$ and vary latitude $$\theta$$. Taking $$\lambda = 1$$ and $$\mu = 0$$ reveals a directional derivative of

$$M_\theta(\theta,\phi)p = (0,-x\cos\theta\cos\phi - y\cos\theta\sin\phi - z\sin\theta)$$

in the $$(1,0)$$ direction. In particular, the $$x$$-coordinate of $$\pi(p)$$ does not change when only $$\theta$$ is changed, which makes sense since we view this as tilting the plane $$\Pi$$ up or down. However, the $$y$$-coordinate changes at a rate precisely equal to $$-\tau(\theta,\phi) \cdot p = -N \cdot p = \tau(-\theta,\phi + \pi) \cdot p$$ (since $$\tau$$ gives points on $$S^2$$). For nonzero $$p$$, this is zero precisely when $$p$$, or equivalently $$p/\lVert p\rVert \in S^2$$, is orthogonal to $$N \in S^2$$, the unit normal vector to the plane of projection $$\Pi$$. This holds when $$N \in T_{p/\lVert p\rVert}S^2$$; if $$\tau(\mathbb R \times \{\phi\}) \subseteq T_{p/\lVert p\rVert}S^2$$, then this occurs for every latitude $$\theta$$, but otherwise, $$\tau(\mathbb R \times \{\phi\})$$ is a circle on $$S^2$$ and intersects $$T_{p/\lVert p\rVert}S^2$$ for precisely one latitude $$\theta$$ (modulo $$\pi$$). From this, we conclude that for principal latitudes $$\theta$$, if $$p/\lVert p\rVert = \pm(N \times \tau(\theta + \pi/4,\phi))$$, $$\pi(p)$$ is always fixed when varying latitude $$\theta$$ (the directional derivative is zero); otherwise, there is precisely one latitude $$\theta$$ (or two, whence $$\theta = \pm\pi/2$$) for which $$\pi(p)$$ has velocity zero.

The above observations agree with a direct calculation: the curve in $$\mathbb R^2$$ that $$\pi(p)$$ traces for fixed longitude $$\phi$$ is

$$\beta_p : \mathbb R \to \mathbb R^2, \quad \beta_p(t) = (\underbrace{-x\sin\phi + y\cos\phi}_{\text{constant}},\underbrace{-x\sin t\cos\phi - y\sin t\sin\phi + z\cos t}_{\text{trigonometric with period}\ 2\pi}).$$

Now, let us consider what happens to $$\pi(p)$$ when we fix latitude $$\theta$$ and vary longitude $$\phi$$. Taking $$\lambda = 0$$ and $$\mu = 1$$ gives a directional derivative of

$$M_\phi(\theta,\phi)p = (-x\cos\phi - y\sin\phi,x\sin\theta\sin\phi - y\sin\theta\cos\phi)$$

in the $$(0,1)$$ direction. A direct calculation gives that the curve in $$\mathbb R^2$$ that $$\pi(p)$$ traces for fixed latitude $$\theta$$ is

$$\delta_p : \mathbb R \to \mathbb R^2, \quad \delta_p(t) = (-x\sin t + y\cos t,-x\sin\theta\cos t - y\sin\theta\sin t + z\cos\theta);$$

the above directional derivative is simply $$\dot\delta_p(\phi)$$. By trigonometry, we know that letting $$T = t + \cos^{-1}(y/\sqrt{x^2 + y^2})$$,

$$\delta_p(t) = (\sqrt{x^2 + y^2}\cos T,-\sin\theta\sqrt{x^2 + y^2}\sin T + z\cos\theta);$$

this is clearly an ellipse (with period $$2\pi$$) with axis lengths $$\sqrt{x^2 + y^2}$$ and $$\lvert\sin\theta\rvert\sqrt{x^2 + y^2}$$, oriented negatively (clockwise) whenever principal latitude is positive (and positively if principal latitude is negative). Additionally, it has 4 vertices by Example 6.3 of chapter 4 (as long as $$\lvert\sin\theta\rvert \neq 1$$ and both axis lengths are nonzero); these vertices correspond to locations where the $$x$$ or $$y$$-coordinate of $$\pi(p)$$ is greatest or smallest. In summary, we see that for fixed latitude $$\theta$$, projected points move in an elliptic shape (in a clockwise direction when viewed from with positive principal latitude); this agrees with the intuition that as we increase longitude $$\phi$$, in order for the normal $$N$$ to the plane of projection $$\Pi$$ to point "into the screen", points must rotate _clockwise_ about the projected $$z$$-axis.

<!--- ### Further differential geometry of the projection

Recall that the projection $$\pi : \mathbb R^3 \to \mathbb R^2$$ is a linear map, so for a point $$p \in \mathbb R^3$$, $$D_p\pi : T_p\mathbb R^3 \to T_{\pi(p)}\mathbb R^2$$ is the linear map given by the matrix $$D\pi = M$$ (see (*) above), by Proposition 2.30 of chapter 1. But $$\pi$$ restricts to a map $$S \to \mathbb R^2$$ of surfaces, so for $$p \in S$$ and $$v = \lambda\sigma_u + \mu\sigma_v \in T_pS$$, it follows that $$D_p\pi(v) = \lambda M\sigma_u + \mu M\sigma_v$$. This tells us exactly how curves and tangent vectors in $$S$$ behave after the projection onto $$\mathbb R^2$$.

This also tells us that wherever there is an open neighbourhood $$V$$ of $$p \in S$$ such that $$\pi$$ restricts to a local diffeomorphism (so that $$\mathbb Rho := \pi|_V \circ \sigma$$ is a surface patch), $$\pi$$ induces a basis $$\{M\sigma_u,M\sigma_v\} = \{\pi(\sigma_u),\pi(\sigma_v)\}$$ of $$T_{\pi(p)}\pi(V) = \mathbb R^2$$ (see (*) for formula). Since $$\tilde S = \pi(V) \subseteq \mathbb R^2$$, the second fundamental form and Weingarten maps of $$\pi(V)$$ do not exist.

The second fundamental form of $$\pi(V) \subseteq \mathbb R^2$$ is identically zero since (thus Gaussian/mean/principal curvatures are all zero).\footnote{See Example 2.10 and Exercise 1 from MTH3110 chapter 10 notes.} Thus, the matrix of the Weingarten map of $$\pi(V)$$ is also the zero matrix.

Now, for any $$p \in S$$, let $$\mathbb Rho = \pi \circ \sigma$$; this may or may not be a regular chart for $$\mathbb R^2$$. Note that $$\mathbb Rho_u = (D\pi)\sigma_u = M\sigma_u$$ and $$\mathbb Rho_v = M\sigma_v$$ by the chain rule, so we have the coefficients of a bilinear form $$\tilde g_{\pi(p)}$$ given by

$$\tilde E = \mathbb Rho_u \cdot \mathbb Rho_u = \sigma_u^\top M^\top M \sigma_u, \quad \tilde F = \mathbb Rho_u \cdot \mathbb Rho_v = \sigma_u^\top M^\top M \sigma_v, \quad \tilde G = \mathbb Rho_v \cdot \mathbb Rho_v = \sigma_v^\top M^\top M \sigma_v,$$

where (from (*))

$$M^\top M =
\begin{pmatrix}
    \sin^2\theta\cos^2\phi + \sin^2\phi & -\cos^2\theta\cos\phi\sin\phi & -\cos\theta\sin\theta\cos\phi \\
    -\cos^2\theta\cos\phi\sin\phi & \sin^2\theta\sin^2\phi + \cos^2\phi & -\cos\theta\sin\theta\sin\phi \\
    -\cos\theta\sin\theta\cos\phi & -\cos\theta\sin\theta\sin\phi & \cos^2\theta
\end{pmatrix}.$$

If $$\mathbb Rho$$ is a local diffeomorphism, the Riemannian metric $$\tilde g_{\pi(p)}$$ of $$\tilde S = \pi(V)$$ at $$\pi(p)$$ (given the chart $$\mathbb Rho$$) has coefficients $$\tilde E,\tilde F,\tilde G$$ above.\footnote{See page 13 of MTH3110 chapter 9 notes.} This can differ from the standard representation of the metric on $$\mathbb R^2$$, i.e. the identity with respect to $$\{e_1,e_2\}$$, but shows how $$\pi$$ preserves the metric from $$S$$. In fact, the Riemannian metric $$g_p$$ of $$S$$ at $$p$$ is the pullback $$g_p = \pi^* \tilde g_{\pi(p)}$$ of $$\tilde g_{\pi(p)}$$ at $$\pi(p)$$.\footnote{See page 14 of MTH3110 chapter 9 notes.}

Also, from these quantities, which can be explicitly computed for different surface charts $$\sigma$$, we can easily check whether $$\pi$$ is a local diffeomorphism ($$\tilde E\tilde G - \tilde F^2 \neq 0$$), a local isometry ($$(E,F,G) = (\tilde E,\tilde F,\tilde G)$$), conformal ($$(E,F,G) = \lambda(\tilde E,\tilde F,\tilde G)$$ for some function $$\lambda > 0$$), or equiareal ($$EG - F^2 = \tilde E\tilde G - \tilde F^2$$).\footnote{See page 38 of MTH3110 chapter 9 notes. Specific examples subject to further investigation.} By Gauss's Theorema Egregium, the Gaussian curvature $$K$$ of a surface is invariant under local isometry.\footnote{See page 1 of these lecture notes from the University of Regina, by A.-L. Mare: \url{http://uregina.ca/~mareal/cs6.pdf}.} Since $$K = 0$$ for the plane $$\mathbb R^2$$,\footnote{See Example 2.10 of MTH3110 chapter 11 notes.} it follows that if $$S$$ does not have zero Gaussian curvature, then $$\pi : S \to \mathbb R^2$$ is not a local isometry. --->

This concludes our analysis of the 2-dimensional visualisation of surfaces in $$\mathbb R^3$$ on Desmos. We saw some commentary on the derivation of the projection, using some linear algebra. Then we proceeded to analyse how curves are represented in the plot, as a "wire-frame", and finally, we analysed the effect of changing latitude and longitude on the positions of points in the plot, rounding off a treatment of the algebraic, analytic, and geometric properties of the visualisation.

<!--- Finally, we considered the differential geometry of curves and the projection map itself, rounding off a treatment of the algebraic, analytic, and geometric properties of the visualisation. --->

### Acknowledgements

I would like to acknowledge Dan Mathews for giving useful feedback (especially with respect to interpreting the effect on changing perspective on the position of points) and verifying the procedure used to derive the projection matrix. Errors in my initial formula for the projection were also corrected through discussion and testing with various members of the [Maths @ Monash Discord server](http://discord.gg/invite/hx63ZwSXBg).
