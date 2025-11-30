---
layout: post
title: 'The small scale structure of axion dark matter'
---

High-resolution lattice and N-body simulations of axion dark matter on sub-galactic scales and implications for terrestrial experiments.

Highlights:
- <strong>Stage I</strong>: MPI/OpenMP lattice simulations with resolutions up to $$8192^3$$ grid sites. <a href="https://github.com/veintemillas/jaxions" target="_blank"><i class="fa fa-github" aria-hidden="true"></i></a>

- <strong>Stage II</strong>: MPI N-body simulations with resolutions up to $$1024^3$$ particles. <a href="https://github.com/gpierobon/MCgadget4" target="_blank"><i class="fa fa-github" aria-hidden="true"></i></a>
 
- <strong>Stage III</strong>: Monte Carlo simulations with up to $$10^6$$ orbits of dark matter-star interaction. <a href="https://github.com/gpierobon/AxionStreams" target="_blank"><i class="fa fa-github" aria-hidden="true"></i></a>


<br>


{% include image2.html image="projects/miniclusters/timeline.jpg" %}

<br>

For the first time in the literature we addressed with high resolution the spatial distribution of axion dark matter. [^1] [^2] [^3] [^4]


#### Stage I

As displayed above, we start our simulations deep in the early Universe by solving the full relativistic <strong>Klein-Gordon</strong> equation with the non-linear potential which gives rise to a newtork of topological defects, namely cosmic string and domain walls. In this first stage, we run simulations with grids of up to $$8192^3$$ sites, which corresponds to tens of TBs of RAM. This can only be achieved in the largest supercomputing faciilities. Overall, we carried out $$\mathcal{O}(100)$$ simulations with a baseline $$3072^3$$ resolution on the [Gadi](https://nci.org.au/our-systems/hpc-systems) HPC facility at NCI Australia. All simulations have been performed using [jaxions](https://github.com/veintemillas/jaxions).


Below, a visualisation of a lattice simulations ($$3{\rm D}\to 2{\rm D}$$ projection) of a collapsing string-wall network and subsequent dark matter production, performed on Gadi.


{% include image2.html image="projects/miniclusters/n6.gif" %}


<br>
<br>
<br>

#### Stage II

In the second stage, we continue the simulation by solving the Schrödinger–Poisson system in the non-relativistic limit until gravitational effects become increasingly important. Owing to the Schrödinger–Vlasov correspondence,[^5] we can then transition to particle-based simulations. For this purpose, we modify the [gadget-4](https://wwwmpa.mpa-garching.mpg.de/gadget4/) code and follow the formation of small clusters and their surrounding halos. Codes and analysis can be found in the repositories [MCgadget4](https://github.com/gpierobon/MCgadget4) and [AxionMC](https://github.com/gpierobon/AxionMC).


Below, a volume rendering of an N-body simulation with $$512^3$$ particles using the [yt](https://yt-project.org/) library, and carried out on Gadi.  
{% include image2.html image="projects/miniclusters/render.gif" width="10" %}



<br>

#### Stage III


In the final stage, we extrapolate the substructure distribution to the present day. Here, we model the small clusters as point particles orbiting the Galactic centre and interacting with forming stars. Tidal stripping can fully disrupt the axion clusters, but the outcome depends sensitively on their concentration. This concentration can be measured in simulations, though current uncertainties remain large. Then, a Monte Carlo simulation sampling over the distribution of cluster parameters—reflecting the existing uncertainties—is used to estimate how much mass is stripped from the clusters, thereby filling the surrounding voids. Analysis of the Monte Carlo pipeline is included in the repository [AxionStreams](https://github.com/gpierobon/AxionStreams). 


{% include image2.html image="projects/miniclusters/mc.png" %}

#### References

[^1]: O'Hare, Pierobon, Redondo, Wong, Axion minivoids and implications for direct detection, [2112.05117](https://arxiv.org/abs/2112.05117)
[^2]: Eggemeier, O'Hare, Pierobon, Redondo, Wong, Axion minivoids and implications for direct detection, [2212.00560](https://arxiv.org/abs/2212.00560)
[^3]: Pierobon, Redondo, Saikawa, Vaquero, Moore, Miniclusters from axion string simulations, [2307.09941](https://arxiv.org/abs/2307.09941)
[^4]: O'Hare, Pierobon, Redondo, Axion minicluster streams in the solar neighbourhood, [2311.17367](https://arxiv.org/abs/2311.17367)
[^5]: Mocz et al., On the Schrodinger-Poisson--Vlasov-Poisson correspondence, [1801.03507](https://arxiv.org/abs/1801.03507)
