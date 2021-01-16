---
layout: post
title: The Basics of Feynman Diagrams, for the Layperson
categories: physics
---

If you have an interest in physics, particularly particle physics, then chances are you've seen a Feynman diagram.

[<img src="{{ site.baseurl }}/images/physics/B-decay.png" alt="Penguin Diagram" style="width: 400px;"/>]({{ site.baseurl }}/images/physics/B-decay.png)

This kind of thing.

But what *are* they, really? How do they help us to do physics? That's what I hope to clear up for you today.

## Not Just a Pretty Face

First thing to note about Feynman diagrams is that they are not simply schematic. They aren't just to show a pictorial representation of what's going on. They are, in fact, an integral part of conducting particle physics calculations. To do so, we use the **Feynman Rules**.

### Feynman Rules: A Quick Introduction

The Feynman rules allow us to calculate a quantity called the "amplitude", or "matrix element". This is a value which essentially tells us the *likelihood* of the diagram in question happening.

A given process (say, electron-muon scattering) can generally proceed by many specific diagrams. For example, here are two diagrams for electron-muon scattering:



Each diagram will have its own probability of happening. The amplitude, $$\mathcal{M}$$, tells us what this probability is (more strictly, it's the squared amplitude, averaged over spins where necessary, that does this).

### Feynman Rules: The Ritual

Now, these Feynman rules come from the underlying quantum field theories describing the process at hand (for example quantum electrodynamics), and will differ based on the interactions in play - QED Feynman rules are different than QCD ones, for example. But they all follow a high-level ritual:

1. External lines: First we take into account the external lines; normally this means spinors (i.e. spin states) and perhaps things like colour states too.
2. Vertices: each vertex gets a factor related to the coupling between the particles involved. The vertex also gets a delta function encoding conservation of four-momentum (i.e. energy and three-momentum); by conserving four-momentum at every vertex, we ensure that it is conserved for the process as a whole. Note that this can still lead to virtual particles being well off their mass shell, as long as the diagram as a whole conserves $$p$$, and the amplitude of the diagram will decrease the further off shell the virtual particles are.
3. Internal lines: each internal line gets a propagator term, dependent on what sort of mediating particle it is, as well as another delta function.
4. Integration: We then integrate over $$q_i$$, the momenta of the internal lines.
5. Cancel the delta-function: We will be left with a factor encoding conservation of energy/momentum; we get rid of this and replace with an $$i$$, since it is taken care of elsewhere.

This leaves us with $$\mathcal{M}$$, which we can then use to calculate cross-sections and decay rates.

## Conclusion

Feynman diagrams are a crucial part of modern particle physics, and are more than simply a schematic representation of the geometry of an interaction. Hopefully this post has given a bit of insight into their power.

My next physics post will probably be a quick introduction to gauge invariance and the Higgs mechanism.