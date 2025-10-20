---
layout: post
title:  "HPC in Julia: ready or not?"
date:   2025-10-02 22:20:00 +0100
tags: [HPC]
draft: true
---
# Introduction
Compuattional astrophysics represents an ever-growing field that tries to simulate the most complicated process
that make our universe such complex place. Since the beginning of century several high profile numerical codes have been created.
Because I am biased to high-energy astrophysics I will discuss here relativistic hydrodynamical simulations used to
describe complex accretion flows.

The most basic and influential code developed in the field is [HARM](https://ui.adsabs.harvard.edu/abs/2003ApJ...589..444G/abstract), 2D code
developed in 2003 to model complex relativistic. It was written in C and parallelized with MPI. Since then, many things have
changed in HPC. Most importantly, the GPU became de-facto standard tool to run simulations. Due to the sheer complexity of
scientific codes several other tools have been created to help port the code to GPU-s. The most influential
tool is [KOKKOS](https://github.com/kokkos/kokkos) - performance portability layer. It allowed to easily port most of numerical-heavy
codes to GPUs resulting in several codes including [AthenaK](https://github.com/IAS-Astrophysics/athenak). Move to kokkos
does not necessarily made life of scientists easier, each of modern kokkos codes still require enourmous amounts of code to work
properly. Especially, the bar to write own GRMHD code is still quite high. This post describes the undertaken efforts
to lover the bar and create a platform to build production-ready HPC code that would be easy to hack and modify.

# Why Julia? 
Julia have became one of more interesting languages in recent decade. It is based on LLVM to compile code in a JIT manner.
Hence, it promises (and delivers) speed comperable with the C/C++. Moreover, It has built in support for linear algebra
(think about the numpy capabilities in standard library).
