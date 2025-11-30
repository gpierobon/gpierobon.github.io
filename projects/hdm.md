---
layout: post
title: 'Large scale structure and neutrinos'
---

High-resolution N-body simulations large scale structure formation and the impact of neutrinos. <a href="https://github.com/cppccosmo/gadget-4-cppc" target="_blank"><i class="fa fa-github" aria-hidden="true"></i></a>


{% include image2.html image="projects/hdm/hdm_proj.png" %}


Building upon previous works at UNSW,[^1] we ran multiple N-body simulations to assess the impact of neutrinos and other hot relics, i.e. hot dark matter, on the formation of the obserbed large scale structure of the Universe. 

We carried out a suite of simulations which treated the effects of the neutrinos in a hybrid way:[^2] the low-momentum part of the Fermi-Dirac (Bose-Einstein for bosonic hot dark matter) is simulated using mass varying cold particles, like in the case of cold dark matter, while the high-momentum part of the distribution is non-clustering and free-streaming, better suited to semi-analytical linear response treatments. This lets us simulate efficiently and with high fidelity the clustering part of the neutrinos, while mitingating the shot-noise of the fast neutrinos. We perform a suite of N-body simulations with resolution of $$512^3$$ particles for dark matter and $$512^3$$ for each of the clustering "streams" of neutrinos. The largest runs therefore used $$\sim 671$$ million particles. All simulations are carried out and analysed on [Gadi](https://nci.org.au/our-systems/hpc-systems) at NCI. 

The visualisation shows the projected energy density in the cold dark matter (top-left) and the converted streams of neutrinos, which contribute to the gravitational clustering. The slowest stream (top-right) follows the dark matter distribution and shows small scale details, while the bottom row highlights the wash-out of small scales due to increased velocity and free-streaming. Details and further results are found in the [paper](https://arxiv.org/abs/2410.05816)).

Our version of the code gadget4 can be found on github: [cppccosmo/gadget-4-cppc](https://github.com/cppccosmo/gadget-4-cppc)

#### References

[^1]: Chen, Mosbech, Upadhye, Wong, Hybrid multi-fluid-particle simulations of the cosmic neutrino background, [2210.16012](https://arxiv.org/abs/2210.16012)
[^2]: One trick to treat them all: SuperEasy linear response for any hot dark matter in N-body simulations, [2410.05816](https://arxiv.org/abs/2410.05816)
