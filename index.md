---
layout: page
title: CoGAPS
subtitle: (Coordinated Gene Association in Pattern Sets)
hero_image: /_images/hero.png
hero_height: is-fullwidth
---

## Introduction
Coordinated Gene Association in Pattern Sets (CoGAPS) is a technique for latent space learning in gene expression data. CoGAPS is a member of the Nonnegative Matrix Factorization (NMF) class of algorithms. NMFs factorize a data matrix into two related matrices containing gene weights, the Amplitude (A) matrix, and sample weights, the Pattern (P) Matrix. Each column of A or row of P defines a feature and together this set of features defines the latent space among genes and samples, respectively. In NMF, the values of the elements in the A and P matrices are constrained to be greater than or equal to zero. This constraint simultaneously reflects the non-negative nature of gene expression data and enforces the additive nature of the resulting feature dimensions, generating solutions that are biologically intuitive to interpret (Seung and Lee (1999)).

CoGAPS has two extensions that allow it to scale up to large data sets, Genome-Wide CoGAPS (GWCoGAPS) and Single-Cell CoGAPS (scCOGAPS). This package presents a unified R interface for all three methods, with a parallel, efficient underlying implementation in C++.
