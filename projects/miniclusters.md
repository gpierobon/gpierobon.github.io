---
layout: post
title: 'The small scale structure of axion dark matter'
---

High-resolution lattice and N-body simulations of axion dark matter on sub-galactic scales and implications for terrestrial experiments.

<br>

{% include image2.html image="projects/miniclusters/timeline.jpg" %}

<br>

For the first time in the literature we addressed with high resolution the spatial distribution of axion dark matter. [^1] [^2] [^3] [^4]


#### Stage I

As displayed above, we start our simulations deep in the early Universe by solving the full relativistic <strong>Klein-Gordon</strong> equation with the non-linear potential which gives rise to a newtork of topological defects, namely cosmic string and domain walls. In this first stage, we run simulations with grids of up to $$8192^3$$ sites, which corresponds to tens of TBs of RAM. This can only be achieved in the largest supercomputing faciilities. Overall, we carried out $$\mathcal{O}(100)$$ simulations with a baseline $$3072^3$$ resolution on the [Gadi](https://nci.org.au/our-systems/hpc-systems) HPC facility at NCI Australia. 


Below, a visualisation of a lattice simulations ($$3{\rm D}\to 2{\rm D}$$ projection) of a collapsing string-wall network, performed on Gadi.


{% include image2.html image="projects/miniclusters/n6.gif" %}


<br>
<br>
<br>

#### Stage II

In the second stage,we continue our simulation by solving the Schroedinger-Poisson system of equations in the non-relativistic limit until the gravitational effects become increasingly relevant.  
{% comment %}
$$\begin{align}
    i\frac{\partial}{\partial t}\psi&=-\frac{\nabla^2\psi}{2ma^2}+m\Phi\psi\\
    \nabla^2\Phi&=\frac{4\pi G}{a}(\vert\psi^2\vert-\langle\vert\psi^2\vert\rangle),
\end{align}$$
{% endcomment %}


Here follows a volume rendering of an N-body simulation with $$512^3$$ particles using the [yt](https://yt-project.org/) library, and carried out on Gadi.  
{% include image2.html image="projects/miniclusters/render.gif" width="10" %}



<br>

#### References

[^1]: O'Hare, Pierobon, Redondo, Wong, Axion minivoids and implications for direct detection, [2112.05117](https://arxiv.org/abs/2112.05117)
[^2]: Eggemeier, O'Hare, Pierobon, Redondo, Wong, Axion minivoids and implications for direct detection, [2212.00560](https://arxiv.org/abs/2212.00560)
[^3]: Pierobon, Redondo, Saikawa, Vaquero, Moore, Miniclusters from axion string simulations, [2307.09941](https://arxiv.org/abs/2307.09941)
[^4]: O'Hare, Pierobon, Redondo, Axion minicluster streams in the solar neighbourhood, [2311.17367](https://arxiv.org/abs/2311.17367)

