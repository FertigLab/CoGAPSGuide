---

layout: page
title: CoGAPS
subtitle: (Coordinated Gene Association in Pattern Sets)
hero_image: /CoGAPS/images/hero.jpg
<!-- hero_height: is-fullwidth -->
hero_darken: true
show_sidebar: false
<!-- hero_link: https://github.com/FertigLab/CoGAPS
hero_link_text: GitHub Repository -->

---

# Introduction

[![downloads](https://bioconductor.org/shields/downloads/release/CoGAPS.svg)](http://bioconductor.org/packages/stats/bioc/CoGAPS/)
[![Build Status](https://travis-ci.org/FertigLab/CoGAPS.svg?branch=master)](https://travis-ci.org/FertigLab/CoGAPS)

<img src="images/logomedium.png" align="left" style="margin: 0px 15px 0px 0px;" />Non-negative matrix factorization (NMF) is an unsupervised learning method well suited to high-throughput biology. Still, inferring biological processes requires additional post hoc statistics and annotation for interpretation of features learned from software packages developed for NMF implementation.
<p>Here, we aim to introduce a suite of computational tools that implement NMF and provide methods for accurate, clear biological interpretation and analysis. A generalized discussion of NMF covering its benefits, limitations, and open questions in the field is followed by three procedures for the Bayesian NMF algorithm <a href="https://github.com/FertigLab/CoGAPS" target="_blank">CoGAPS</a> (Coordinated Gene Activity across Pattern Subsets). Each procedure will demonstrate NMF analysis to quantify cell state transitions in public domain single-cell RNA-sequencing (scRNA-seq) data of 25,422 epithelial cells from pancreatic ductal adenocarcinoma (PDAC) tumors and control samples. The first demonstrates <a href="https://github.com/FertigLab/pycogaps" target="_blank">PyCoGAPS</a>, our new Python implementation of CoGAPS that enhances runtime of Bayesian NMF for large datasets.</p>
<p>The second procedure steps through the same single-cell NMF analysis using our R CoGAPS interface, and the third introduces a beginner-friendly CoGAPS platform using GenePattern Notebook. By providing Python support, cloud-based computing options, and relevant example workflows, we facilitate user-friendly interpretation and implementation of NMF for single-cell analyses. The expected timing to properly setup the packages and conduct a test run is around 15 minutes, and an additional 30 minutes to conduct analyses on a precomputed result. The expected runtime on the user’s desired dataset can vary from hours to days depending on factors such as the size of the dataset or input parameters.</p>

<center><img width="600" height="309" src="images/figure1.png"></center>
<figcaption>NMF factorizes expression data into lower-dimensional amplitude (A) gene weights matrix and pattern (P) weights matrix whose product approximates the input.</figcaption>
