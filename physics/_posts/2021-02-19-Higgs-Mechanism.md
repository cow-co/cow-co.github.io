---
layout: post
title: "The Higgs Mechanism, for the Layperson"
categories: physics
---

In this post, we're going to cover the Higgs mechanism. We'll be diving into a little bit of depth, conceptually, but will be avoiding a lot of the maths. Hopefully this will ensure it is accessible to the layperson.

So let's hop to it!

## Lagrangian Formulation for Fields

We will start with the Lagrangian formalism. The Lagrangian of a system is a description of its energy state: $$L = T - V$$, where $$T$$ and $$V$$ are the kinetic and potential energies, respectively. This is the classical, particle-based formulation of the Lagrangian. Note that it shows the *difference* between the two kinds of energy; contrast this with the Hamiltonian, which is the *total* energy: $$H = T + V$$. Combining a Lagrangian with the Euler-Lagrange equations (which I will provide here, but you needn't understand the maths)

$$\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q_i}}\right) = \frac{\partial L}{\partial q_i}$$

allows us to find the equations of motion for the system.

We can re-formulate this in order to be appropriate for *fields*. A field is a mathematical object which carries some value at every point in the space; temperature is a scalar field, for example, whilst the magnetic field is a vector field. To get a field version of the Euler-Lagrange equations, we express the derivatives with respect to the *fields* ($$\phi_i$$) and their derivatives, which are themselves functions of space and time, rather than with respect to space and time coordinates (and their derivatives) directly:

$$\partial_\mu\left(\frac{\partial \mathcal{L}}{\partial_\mu {\phi_i}}\right) = \frac{\partial \mathcal{L}}{\partial \phi_i}$$

where we use some Einstein indices, as is customary in relativity.

Generally in quantum field theory, we are "given" the Lagrangian (rather than working it out from the kinetic and potential energies, which may not be particularly well-defined for a field anyway).

## Local Gauge Invariance

Some Lagrangians are invariant (they stay the same) under a transformation of the form

$$\psi \rightarrow e^{i\theta}\psi$$

where $$\theta$$ is some constant phase. We call this a "global" gauge transformation, since it shifts the entire field by a constant amount. But these Lagrangians may *not* be invariant under a "local" gauge transformation, where $$\theta$$ depends on space and time:

$$\psi \rightarrow e^{i\theta(x)}\psi$$

where we use the relativistic convention of having $$x$$ mean all four coordinates of a space-time position. This transformation will generally introduce an extra term (from the derivatives of $$\theta$$) onto our naïve Lagrangian.

Something interesting happens, however, when we *require* that local gauge invariance holds for our Lagrangian. This will require us to put in a term to compensate for that which pops out of the $$\theta$$ derivatives. Specifically, we are obliged to introduce *new fields* (called "gauge fields"). These fields themselves must have even more terms, which correspond to the "free" Lagrangians for those fields. So what we are left with is essentially:

- Free Lagrangian(s) for our original field(s)
- Some gauge-transformation-compensating term(s) involving some combination of new and original fields
- Free Lagrangians for the gauge field(s)

Now, we've treated $$\theta$$ so far as if it's a scalar (just a number); but we can make it a vector or tensor or whatever.

So, what we have here is the foundations of our Feynman Rules that we saw last time: the propagators come from the free-field Lagrangians, and the vertex factors come from the interaction terms! 

If we look at a real Lagrangian:

$$\mathcal{L} = \left(i\hbar c \bar{\psi}\gamma^\mu \partial_\mu \psi - mc^2 \bar{\psi} \psi\right) - \left(\frac{1}{16\pi}F^{\mu \nu}F_{\mu \nu}\right) + \left(\frac{1}{8\pi}\left(\frac{Mc}{\hbar}\right)^2 A^\nu A_\nu\right) - (q\bar{\psi}\gamma^\mu \psi)A_\mu$$

Firstly, it looks scary, I know. But really, what we see here is "full" Lagrangian for quantum electrodynamics (with a caveat that we'll see in a moment). The first term in brackets describes our free electrons, positrons, and so on (all our charged particles). The second and third bracketed terms are the free-field Lagrangian for the new field that we are obliged to introduce in order to preserve local gauge invariance - those who have electromagnetism will recognise the formulation here; these terms describe the photon or the electromagnetic field (whichever way you want to look at it). And finally we have the interaction term, telling us how the photon interacts with charged particles.

I'm going to confess to something now. This Lagrangian is *not* actually locally gauge-invariant. The problem is that term involving $$M$$ (i.e. the photon mass). The $$A^\nu A_\nu$$ factor is not gauge invariant! How do we fix this? Well, we just have to make $$M = 0$$. That is, we make the photon massless. So the massless nature of the photon has dropped out of our requirement for gauge invariance. The same argument applies to the gluons in QCD.

But if mass terms break our gauge invariance, how then do we account for the weak mediators (the $$W$$s and $$Z$$), which are massive?

## Spontaneous Symmetry-Breaking

This is where things get subtle. So I'm going to really gloss over a whole bunch of the rigorous stuff here. All you need to know for this is that, in order to apply our Feynman calculus, we must find the ground state (the state with lowest potential $$\mathcal{V}$$) of the system. But some systems have *multiple* ground states - the ground state is said to be "degenerate". So we have to *choose* one of these. 

By choosing a ground state, we "break" the symmetry of the system; a Lagrangian for which a particular symmetry holds may no longer have that symmetry once we rewrite it in terms of our chosen ground state. We call this type of symmetry-breaking "spontaneous", because no external agent has instigated it.

By applying this technique to our Lagrangian, we get a massive field (which is fine), but also some *massless* (so-called "Goldstone") bosons. Which is less good.

## The Higgs Mechanism

We've been obliged to introduce even more fields, some of which are *massless*, and we still don't have anything that looks like our massive weak mediators. What do we do now?! 

Local gauge invariance, is what. It turns out that we can *choose* a gauge (that is, choose a specific transformation) such that the Goldstone bosons disappear entirely, and our weak mediators pop out as gauge fields! Remember, because our Lagrangian is invariant under such transformations, we are completely free to do this. 

You might consider this as essentially "rephrasing" the problem, to "absorb" the Goldstone bosons into an adjusted form of the massive boson. We do this to match what we observe in reality (i.e. that none of these Goldstone bosons exist) - if we *did* observe the Goldstone bosons, we'd just do away with the gauge transformation.

Now, as you may have guessed, this massive boson that we are left with is the famous Higgs boson. And we can now see why it is described as "giving mass to" other particles (it has couplings to the quarks and leptons as well, "granting" them mass): when we introduce this Higgs mechanism, the particles to which it couples gain mass terms.

## Wrap-up

Hopefully this was an interesting introduction to the Higgs mechanism. If you want to read a more rigorous introduction, then Griffiths' Introduction to Elementary Particles is a good shout; this post is based on his description of the Higgs mechanism, but with the maths mostly stripped out and so on.

I don't know what I'll cover next. I'm thinking of starting a weekly paper-summarisation post, picking a pre-print from ArXiV and going through it a bit.