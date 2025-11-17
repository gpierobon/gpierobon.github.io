---
layout: post
title: 'Microwave cavities and spectral signatures of dark matter'
---

Can a high resolution analysis enhance the search for axion dark matter using microwave cavities? [^1]

{% include image.html image="projects/haloscopes/thumbnail.jpg" text="Read the paper" url="https://arxiv.org/pdf/2509.14874"%}

Microwave cavities are the fundamental tool in experimental searches for axion dark matter, particularly in so-called "haloscope" experiments such as the pioneering <strong>A</strong>xion <strong>D</strong>ark <strong>M</strong>Atter E<strong>X</strong>periment ([ADMX](https://depts.washington.edu/admx/)). In the presence of a strong static magnetic field, axions in the dark matter halo can convert into photons via Primakoff effect if the axion Compton frequency matches a resonant mode of the cavity, inducing a resonance.

Such cavities are engineered to have extremely high quality factors $$Q$$ and include tuning mechanisms to change the resonant frequency, so that experiments can “scan” over different possible axion masses (frequencies). State-of-the-art haloscope designs incorporate quantum-limited amplifiers,[^2] microwave photon counters,[^3] squeezed-state measurements,[^4] and high-performance cryogenic systems to reduce noise so that even an expected power from axion conversion on the order of $$10^{-22}$$ watts can become detectable. Current best sensitivies lie in the $$\mathcal{O}(\mathrm{GHz})$$ cavity frequency range, see [AxionLimits](https://cajohare.github.io/AxionLimits/).


In the standard analysis of cavity experiments the ultra-fine-grained dark matter substructure is usually considered irrelevant and undetectableand. Indeed, the signal is typically modelled as a smooth background in the space of velocities, i.e. in the frequency dependence. We argue however that by considering the distribution of dark matter substructure, not only once could detect its features in haloscope experiments, but that it may enhance the sensitivity. In the case of axions, the local distribution of dark matter is expected to feature a large number of spatially overlapping "streams" which can locally enhance the signal-to-noise ratio in some frequency bins, if the timeseries is analysed with a high-enough frequency resolution. [^5] 

The spectral shape can be constructed as 

$$\langle S(\omega) \rangle \propto \int_0^\infty {\rm d}v f(v)\, {\rm sinc}^2\left( \frac{1}{2}(\omega_v - \omega)T\right),$$

where $$f(v)$$ is the underlying speed distribution of the dark matter, $$\omega_v = m_a(1+v^2/2)$$, with $$m_a$$ the axion mass, and $$\omega$$ is the spectral frequency. This motivates ongoing high-resolution analyses of axion data by haloscope collaborations, which have the potential to reveal evidence of the QCD axion with increased sensitivity. 
 
<br>
Spectral features of smooth background (<strong>left</strong>) and an ensemble of dark matter streams (<strong>right</strong>), as a function of the integration time.
{% include image2.html image="projects/haloscopes/streams.gif" %}

<br>

Check out the [2023](https://arxiv.org/abs/2311.17367) and [2025](https://arxiv.org/abs/2509.14874) papers for our main results and additional details.


<br>


#### References

[^1]: O'Hare, Pierobon, Fine-grained dark matter substructure and axion haloscopes, [2509.14874](https://arxiv.org/abs/2509.14874)
[^2]: Quiskamp et al., Near-quantum-limited axion dark matter search with the ORGAN experiment around 26 $$\mu$$eV, [2407.18586](https://arxiv.org/abs/2407.18586) 
[^3]: Braggio et al., Quantum-enhanced sensing of axion dark matter with a transmon-based single microwave photon counter, [2403.02321](https://arxiv.org/abs/2403.02321) 
[^4]: Backes et al., A quantum-enhanced search for dark matter axions, [2008.01853](https://arxiv.org/abs/2008.01853)
[^5]: O'Hare, Pierobon, Redondo, Axion streams in the solar neighbourhood, [2311.17367](https://arxiv.org/abs/2311.17367)


