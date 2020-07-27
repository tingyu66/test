---
title: 'exafmm-t'
tags:
  - C++
  - Python
  - fast multipole method
  - high performance computing
authors:
 - name: Tingyu Wang
   orcid: 0000-0003-2520-0511
   affiliation: 1
 - name: Rio Yokota
   orcid: 0000-0001-7573-7873
   affiliation: 2
 - name: Lorena A. Barba
   orcid: 0000-0001-5812-2711
   affiliation: 1
affiliations:
 - name: The George Washington University
   index: 1
 - name: Tokyo Institute of Technology
   index: 2
date: 21 July 2020
bibliography: paper.bib
---

# Summary

The fast multipole method (FMM), recognized as one of the top 10 algorithms from the 20-th century,
is an algorithm that reduces the complexity of N-body problems from $\mathcal{O}(N^2)$ to $\mathcal{O}(N)$ by approximating far-range interactions in a hierarchical way.
Originally developed for fast evaluation of the gravitational potential field, the FMM and its variants now have found many applications in different fields.

Exafmm-t is a parallel fast multipole method (FMM) library for solving N-body problems in 3D.
It implements the kernel-independent fast multipole method (@yingKernelindependentAdaptiveFast2004) (KIFMM) and runs on multicore architectures. 
Currently, it supports both potential and force calculation of Laplace, low-frequency Helmholtz and modified Helmholtz (Yukawa) kernel; furthermore, users can add other non-oscillatory kernels with only modest effort in exafmm-t's framework.
Exafmm-t is a header-only library written in C++ and also provides Python APIs using pybind11 (@pybind11).

Greengard and Rokhlin pioneered the original FMM work (@GreengardRokhlin1987) in 1987.
Over the past few decades, a plethora of high-performance FMM implementations (@yokotaFMMBasedDual2013, @malhotraPVFMMParallelKernel2015, @blanchardScalFMMGenericParallel2015, @choiCPUGPUHybrid2014) have emerged.
However, many of them are geared towards specific research needs complicated to understand.
less accessible to other users
This motivates us 

Our work combines techniques from several past efforts, with regards to data structures, algorithmic tricks, and memory optimizations.

Exafmm-t is designed to be standard, fast and lean.
First, it only uses C++ STL containers and only depends on mature math libraries: BLAS, LAPACK and FFTW3.
Second, exafmm-t is concise but highly optimized. The core library consists of around 6,000 lines of code.
In addition to multi-threading, we further speed up the near-range interactions using SIMD vectorization (SSE/AVX/AVX-512); we use the cache optimization proposed in PVFMM to improve performance of the far-range interactions.
If offers high-level Python APIs.

We are currently integrating exafmm-t into Bempp-cl, an open-source boundary element package in Python.
It uses FMM to reduce time and memory cost of solving the dense linear systems arising in boundary element applications.

# References
