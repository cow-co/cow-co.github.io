---
layout: post
title: High-Energy Physics Simulation Basics
categories: physics
---

This is a little post about simulations in high-energy physics research (think places such as CERN). We'll go through why there is a need for simulations, and broadly how the simulations work. Let's hop to it!

## Why Simulation?

Simulations in particle physics are of great importance, since they allow researchers to make predictions about what they need to look for in various configurations of Nature. For example, a researcher may wish to see what the distribution of some observable quantity is, under the assumption that some model is true (let's say Supersymmetry - SuSy). The researcher would then run a simulation of some events, using parameters from the theoretical model, and the results will guide them in where they would need to look in order to find evidence for or against the given model.

They are also useful in development of experimental techniques. Taking real-life data is expensive (time- and money-wise), so it is very useful to be able to test your techniques on simulated data, before you unleash them on real data. Particularly if your techniques require changes to things like triggers, which require a re-take of real-life data (as opposed to techniques which can be run on data already taken).

So now we know why simulations are important. But how do they actually work?

## Monte Carlo Simulation

The core of particle physics simulation is "Monte Carlo". This is the broad method by which events are simulated. In simple terms, a Monte Carlo simulation generates a random number from some distribution, then makes some decision based on the value of that random number. For example, we could pull from a uniform distribution between [0, 1] to simulate a coin toss, with us calling Heads if `x > 0.5`, and tails if `x <= 0.5`.

By this general method, our simulations generate events, complete with particle momenta, energies, and so on. These will then be fed through the rest of the simulation pipeline.

## The Simulation Pipeline

The flow of a particle physics simulation will generally proceed like so:

1. Event generation. This represents the core physics processes (e.g. at the beam interaction point), both hard and soft (where appropriate) - i.e. high and low energy - and including hadronisation and jet production where necessary.
2. Detector simulation. In this stage, we simulate how the particles propagate through the detector itself, which includes interactions with the detector materials, and any interactions with fields (such as magnetic fields) in the detector space.
3. Digitisation. The analogue response of the detector components to the particles they detect is turned into a digital signal, so this must be modelled too, since there will be some loss/uncertainty in how that conversion is made.

At this point, the "simulation" is done, and the output can then be fed through the same data pipeline as real data would be.

## Further Reading

- [Monte Carlo Simulation Techniques](https://indico.cern.ch/event/115514/contributions/68481/attachments/50952/73307/simulationTechniques.pdf)
- [LHCb Data Flow (LHC Run 2)](https://lhcb.github.io/starterkit-lessons/first-analysis-steps/run-2-data-flow.html)
- [Pythia (event generation)](http://home.thep.lu.se/Pythia/)
- [MadGraph (matrix elements for event generation)](https://cp3.irmp.ucl.ac.be/projects/madgraph/)
- [EvtGen (event generation for flavour physics)](https://evtgen.hepforge.org/)
- [Geant4 (_de facto_ standard for detector simulation)](https://geant4.web.cern.ch/)
