---
layout: post
title: "Weekly Paper Summary - Week of 20/06/21"
categories: physics
---

Hello! After having a good time with last week's review, I'm going to keep it up this week with another HEP paper-review. Enjoy!

# The Shortlist

- [First neutrino interaction candidates at the LHC](https://arxiv.org/pdf/2105.06197.pdf)
- [Regarding the distribution of glue in the pion](https://arxiv.org/pdf/2106.08451)
- [All-flavor constraints on nonstandard neutrino interactions and generalized matter potential with three years of IceCube DeepCore data](https://arxiv.org/pdf/2106.07755)
- [Muon $$g-2$$: current status](https://arxiv.org/pdf/2106.06723)
- [Search for R-parity-violating supersymmetry at ATLAS](https://arxiv.org/pdf/2106.09609.pdf)

## The Chosen Paper

This week, we'll be looking at the last paper in that list. It was a close choice between that and the first in the list (direct detections of collider neutrinos are a pretty big step forward in that sector), but I figured I have more to talk about with the R-parity paper.

# Summary

## Some Background

### Supersymmetry

Chances are that you've at least heard of supersymmetry (SUSY) if you're reading this. It is a model which seeks to extend the Standard Model (SM) of particle physics, in order to close up some holes which exist in the SM, most notably the "Hierarchy Problem" - the issue that gravity is so much weaker than other fundamental interactions (hierarchy problems in the general sense are problems where there seems to be a great discrepancy between one parameter and others of like kind). It solves this problem by giving every fermion a matching "superpartner" boson, and *vice versa*. This cancels out some quadratic corrections that we would expect to make the Higgs mass large.

### R-Parity

An issue comes into play, however, when we introduce all these extra particles. Namely, they would make the proton decay comparatively quickly - something which we obviously do not see (since it would cause *all* atoms to decay in similarly quick time). So one of the simpler ways to deal with this is to introduce some symmetry which, when conserved, prevents (or at least discourages) decay from SM particles into SUSY particles. This is R-parity. Interestingly, it also prevents the decay of the lightest supersymmetric particle - thereby making that particle a promising candidate for dark matter. 

However, R-parity conservation is not a required element of SUSY; SUSY models can be constructed that violate R-parity. 

### Jets

When you have decays that result in quarks in a particle accelerator, a little thing called "colour confinement" comes into play. This is the phenomenon wherein we cannot observe isolated quarks. As two quarks are pulled further apart, they pass a point where it is favourable to spontaneously form two new quarks to join up with the existing ones (we now have two pairs). This process then repeats over and over, the quarks spontaneously forming many hadrons as they propagate away from the original interaction point. This process is called "hadronisation", and results in "jets" of hadrons, which are very distinctive. If you've ever seen the images that CMS put out, visualising the Higgs discovery events, then you'll have seen the jets:

[<img src="{{ site.baseurl }}/images/physics/higgsdisco.png" alt="Higgs Event" style="width: 400px;"/>]({{ site.baseurl }}/images/physics/higgsdisco.png)

(image &copy;CERN [CC-BY-SA-4.0](http://creativecommons.org/licenses/by-sa/4.0/))

Those long green streaks are jets, basically.

The more difficult part of working with jets is finding out what *sort* of jet they are (what quark, exactly). This is called "tagging". In the paper here, $$b$$-tagged jets were particularly important.

## The Paper

The paper we're looking at today presents an update of [a previous analysis](https://arxiv.org/pdf/1704.08493.pdf), with almost 100 fb$$^{-1}$$ more 13 TeV data. Specifically, the analysis looked for R-parity-violating decays resulting in $$\geq$$ one isolated lepton, and a high jet multiplicity (i.e. lots of jets - specifically eight to 15). The simulations used in choosing various parameters for the analysis were simplified SUSY models - the simplification would have allowed the team to generate simulated data and perform analysis in a more optimised way than using more complete models, whilst still retaining the overall character of the resulting distributions (an example of the 80/20 rule). The main backgrounds that needed to be handled were those involving top-quark pair production; an interesting little catching point was that the high jet multiplicity regime is difficult to calculate in SM theory, so predictions had to be made via extrapolating existing medium multiplicity data.

Interestingly in this analysis, *two* different approaches were used: one more generic, and one tailored to a specific scenario of SUSY particle production.

1. The first (more generic) analysis approach involved binning (that is, putting into bins, not throwing away) events with particular numbers of jets, and seeing how the distributions of the events ($$x$$-axis: number of $$b$$-tagged jets, $$y$$-axis, number of events) in each bin compared with the background.
2. The more specific approach was tailored towards electroweak SUSY partners (electroweakinos) by adding in a neural network discriminant as an extra variable.

The analysis found no significant excess over the predicted SM results, but (as always) it has placed tighter constraints on the masses of various SUSY particles in different scenarios.

## Conclusion

And that is it. Hopefully it was interesting; you got to see a little supersymmetry in this one! I wonder what we'll be looking at next week...I'll see you then! Also, look out for another (long overdue) post soon. Probably tomorrow.

