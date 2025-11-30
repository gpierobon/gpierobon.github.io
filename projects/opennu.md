---
layout: post
title: 'Open Quantum Systems meet the C\(\nu\)B'
---

Numerical treatment of all dissipative sources and forecasted experimental sensitivity for relic neutrino detection in next-generation NMR setups. <a href="https://github.com/gpierobon/OpenNu" target="_blank"><i class="fa fa-github" aria-hidden="true"></i></a>
<br> 


{% include image2.html image="projects/opennu/oqs1.jpg" %}


In this project[^1] we explored the effects of the <strong>Cosmic Neutrino Background</strong> (C$$\nu$$B) in future state-of-the-art NMR experiments like [CASPEr](https://budker.uni-mainz.de/?page_id=7). [^2] While such experiment is designed to work near the ground state to find wave-like dark matter, a similar setup can be sensitive to superradiant interactions of cosmic relics, such as non-relativistic neutrinos produced in the early Universe. Like in the case of open quantum systems, we derive under the Born-Markov approximation the <strong>Lindblad</strong> master equation:

$$
\frac{\mathrm{d} \rho_S}{\mathrm{d}t} =-{\rm i}[H_I, \rho_S]+\sum_k \gamma_k \mathcal{D}_{O_k}[\rho_S(t)],
$$

where the system of interest is an ensemble of nuclear spins and the neutrinos act as a dissipative Markovian environemnt (bath) that could be measured. We modelled such neutrino tunable noise along with all the other noise sources and limitations in NMR experiments. Notably:

- Collective emission and pumping, induced by the neutrinos with rates $$\gamma_{\pm}N^2$$
- Local dephasing ($$T_2$$ effects) and relaxation ($$T_1$$ effects)
- Partial polarisation achieved with spin-exchange optical pumping (SEOP) using, e.g., $$^{129}$$Xe spins[^3]


We solve the master equation for the reduced density matrix in the presence of collective effects in the symmetric subspace for values as large as  $$N\sim 10^4$$ using a state-of-the-art `C++` [solver](https://github.com/gpierobon/OpenNu). Incoherent effects can be also be modeled assuming permutational invariance, as implemented in the `qutip`[^4] library. Nevertheless, we derived a set of fast approximate solutions which converge to sub-permille level with `qutip` solutions and work for arbitary large values of $$N$$, including all dissipative effects. 


<br>
Below, effects of local interactions such as dephasing are visualised in the Dicke basis $$\vert j, m\rangle$$ as a loss of coherence.

<br>
Starting from the <strong>Equatorial Coherent Spin State</strong> $$\vert{\rm ECSS}\rangle=\frac{1}{\sqrt{2}}\Pi (\vert \downarrow\rangle+\vert\uparrow\rangle)$$

{% include image2.html image="projects/opennu/dicke2.gif" %}

<br>
<br>
<br>
Starting from the <strong>Ground State</strong> $$\vert g\rangle=\Pi \vert \downarrow\rangle$$

{% include image2.html image="projects/opennu/dicke.gif" %}
<!--- {% include image.html image="projects/opennu/bloch.gif" text="View presentation" url="https://www.youtube.com/watch?v=NMDLzl0ruZk" %} --->



<br>

Check out in the [paper](https://arxiv.org/abs/2508.20357) our forecast sensitivities. Additional details of the numerical solutions and statistical anaylis are found on github: [OpenNu](https://github.com/gpierobon/OpenNu) and [pyOpenNu](https://github.com/gpierobon/pyOpenNu). A recent recording of my seminar about this project can be found [here](https://www.youtube.com/watch?v=NMDLzl0ruZk").

<br>

#### References

[^1]: Garcia Del Castillo, Pierobon, Sengupta, Wong, Prospects for relic neutrino detection using nuclear spins, [2508.20357](https://arxiv.org/abs/2508.20357)
[^2]: Budker et al., Proposal for a Cosmic Axion Spin Precession Experiment (CASPEr), [1306.6089](https://arxiv.org/abs/1306.6089)
[^3]: Walter et al., Search for axionlike dark matter using liquid-state nuclear magnetic resonance, [2504.16044](https://arxiv.org/abs/2504.16044)
[^4]: [qutip.org/](https://qutip.org/)
