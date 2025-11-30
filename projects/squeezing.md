---
layout: post
title: 'Quantum spin squeezing and cosmic relics'
---

Can quantum spin squeezing in NMR systems help the search for new particles? 

{% include image2.html image="projects/squeezing/squeeze_img.png" max_width="80%"%}


<br>
<br>
 
We consider an ensemble of $$N$$ identical two-level systems (spins) coupled to a single-mode cavity field. The system is described by the Tavis-Cummings Hamiltonian (assuming the rotating-wave approximation and $$\hbar = 1$$):
\begin{equation}
    H = \omega_c a^\dagger a + \omega_s J_z + g \left( a^\dagger J_- + a J_+ \right),
\end{equation}
where $$\omega_c$$ is the cavity mode frequency, $$\omega_s$$ the spin transition frequency, $$a$$ $$(a^\dagger)$$ is the annihilation (creation) operator for the cavity mode, and $$J_\pm = \sum_{i=1}^N \sigma_\pm^{(i)}$$ are collective spin raising and lowering operators. The collective operators obey angular momentum algebra with total spin $$J = N/2$$. In the dispersive regime, the detuning
\begin{equation}
    \Delta = \omega_c - \omega_s
\end{equation}
is large compared to the collective coupling, i.e., $$|\Delta| \gg g \sqrt{N}$$. In this limit, real energy exchange between the spins and the cavity is strongly suppressed, but virtual photon exchange leads to effective spin–spin interactions. The effective Hamiltonian contains a non-linear term, the so-called one-axis twisting (OAT) Hamiltonian, first proposed by Kitagawa and Ueda, which is known to generate spin-squeezed states
\begin{equation}
    H_{\text{OAT}} = \chi J_z^2.
\end{equation}

Under collective (coherent) effects of cosmic neutrinos or axion-like dark matter, the variance increases in time and  

{% include image2.html image="projects/squeezing/squeeze_t.png" %}

{% include image2.html image="projects/squeezing/squeeze.gif" %}
