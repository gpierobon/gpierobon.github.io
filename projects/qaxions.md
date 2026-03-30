---
layout: post
title: 'Wave dark matter simulations'
---

<div style="display: flex; gap: 10px;">
  {% include image2.html image="projects/qaxions/frame0.png" max_width="80%" %}
  {% include image2.html image="projects/qaxions/frame1.png" max_width="80%" %}
</div>

To study the behaviour of wave dark matter, I developed `qaxions` is a high-performance simulation code. 
It solves the Schrödinger-Poisson system of equations on a 2D or 3D lattice, capturing the quantum wave-like
dynamics that make axions and similar particles distinct from heavier dark
matter models. The code is written in C++ and designed to scale from a laptop
to HPC clusters, with OpenMP multithreading and optional GPU acceleration
via CUDA that delivers up to 40× speedups over CPU-only runs. Python bindings
via `pybind11` make it easy to set up simulations, process outputs, and
interface with existing analysis workflows without leaving Python. `qaxions` is
intended as a flexible and accessible entry point for researchers
looking to explore ultralight dark matter dynamics on modern hardware.

Check out the online [documentation](https://qaxions-8f911f.gitlab.io/) and the source code
 <a href="https://gitlab.com/gpierobon/qaxions" target="_blank"><i class="fa fa-gitlab" aria-hidden="true"></i></a>
<br> 

#### Code features

- High-performance C++ core
- OpenMP parallelism
- HDF5 and FFTW support
- GPU acceleration with CUDA and cuFFT
- Python bindings via `pybind11`
- Linux and macOS support

