---
layout: post
title: "Weekly Paper Summary - Week of 12/06/21"
categories: physics
---

Hello! Welcome to the first in what I want to make into a series of posts. This series will cover one interesting high-energy physics paper per week. I'll summarise the paper, at roughly the layperson level. Hopefully this will give you a bit of an idea of the direction HEP research is going at the moment. I will shortlist one interesting-looking paper per day from ArXiV, and select from those whichever one I find most interesting.

# The Shortlist

- [A First Next-to-Next-to-Leading Order Study of Three-Jet Production at the LHC](https://arxiv.org/pdf/2106.05331.pdf)
- [Search for active-sterile antineutrino mixing using neutral-current interactions withthe NOvA experiment](https://arxiv.org/pdf/2106.04673.pdf)
- [Measurement of branching fractions and search for CP violation at Belle](https://arxiv.org/pdf/2106.04286.pdf)
- [Observation of the mass difference between neutral charm-meson eigenstates](https://arxiv.org/pdf/2106.03744.pdf)
- [A very high energy hadron collider on the Moon](https://arxiv.org/pdf/2106.02048.pdf)

## The Chosen Paper

I chose the active-sterile mixing paper, primarily because it involves a non-LHC experiment. This makes it a little different than my usual reading. It is also about physics in the neutrino sector, which again I don't usually look at (my interest tends to be more in the flavour/heavy meson sector).

# Summary

## Some Background

### Mixing

"Mixing" is is a broad term that we use to refer to processes where, basically, we have two "forms" of a particle changing back and forth into one another. A classic example is neutral $$K$$ meson mixing, in which the first conclusive evidence for $CP$ violation was found. Mixing in the neutrino sector was conclusive evidence of neutrino masses; this is because the *flavour* eigenstates, which are the eigenstates that take part in the weak processes by which we *detect* them, are *superpositions* of mass states. The neutrinos *propagate* through space as mass eigenstates. What this means is that, because the masses of the neutrino mass eigenstates are different, the *flavour* composition of a group of neutrinos may differ between one point and another, as the group moves through space. 

### "Sterile" Antineutrinos

So-called "sterile" antineutrinos are antineutrinos which do not interact via any Standard Model process (they still have mass - the SM says nothing about gravity). We have indications of their existence, but nothing concrete yet. The first part of this hint is based on results from short-baseline (read: small-scale) experiments; the results are inconsistent with a 3-flavour ($$\bar\nu_{e}$$, $$\bar\nu_{\mu}$$, $$\bar\nu_{\tau}$$) theory. The second indicator (the one which hints to us that the "new" neutrino would be sterile) is that measurements of width of the $$Z^0$$ show that this new antineutrino does not take part in the weak interaction. So, unless the mass of this extra antineutrino is *greater* than about half that of the $$Z^0$$ (highly unlikely), it must be sterile.

### The $$3+1$$ Model

This is the simplest way to incorporate the sterile neutrino into our theory. We basically just add in an extra neutrino to our neutrino mixing matrix (called the PMNS matrix) - this basically accounts for the fact that the new neutrino is assumed to be massive, and will therefore mix with our already-known ones. This introduces some new parameters (phases and mixing angles) which could potentially exhibit $$CP$$ violation.

## The Paper

The present paper describes a search at the long-baseline NOvA experiment. During this analysis, they were looking at *anti*neutrinos; I've treated them interchangeably thus far, but there have been experimental discrepancies in the past between them. So they may not strictly be interchangeable.

The way the experiment works is that there are two detectors looking for (neutral-current) weak interactions: the Near Detector, and the Far Detector. In a 3-flavour scenario, the rate at which such interactions occur is independent of flavour; therefore, it is unaffected by mixing. So the rates detected at both detectors should be the same (within the bounds of randomness and experimental uncertainty, of course). However, if we introduce a sterile flavour, then it (by definition) will not participate in these weak processes. Therefore, as the proportion of sterile antineutrinos changes (due to mixing) we should observe a difference in neutral current rates between the Near and the Far Detector. The experiment is sensitive to mixing angles, phases, and one of the mass splittings; so it's a pretty good way to get some good data on the nature of the mixing (and potentially on $$CP$$ violation).

The analysis used various cuts on the vertex (i.e. interaction) geometry, particularly on where in the beamline/detectors the interaction happens. This helps to reduce backgrounds from, for example, cosmic antineutrinos. The data was then passed through a convolutional neural network (CNN) in order to search for signal.

The analysis showed no indication of oscillations to a sterile antineutrino. But it was able to set constraints on the possible values of some of the parameters that would be involved if such oscillations *were* to occur.

## Conclusion

Well, I hope you found that interesting. Quite a nice little paper about a sector I'm not too too familiar with. I'll see you next week!

