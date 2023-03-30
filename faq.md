---

hero_image: /CoGAPS/images/hero.jpg
<!-- hero_height: is-fullwidth -->
hero_darken: true

---

# FAQ

## What is NMF?

NMF (Nonnegative Matrix Factorization) is a mathematical technique with a long history in the field of genomics for the analysis of bulk RNA sequencing data<sup>1,2</sup>, and it has been widely adopted as a powerful dimensionality reduction tool for single-cell data as well<sup>3,4,5–10</sup>.

## What is CoGAPS?

CoGAPS (Coordinated Gene Activity across Pattern Subsets) is a Bayesian NMF (Nonnegative Matrix Factorization) algorithm. It can be used to perform sparse matrix factorization on any data, and when this data represents biomolecules, to do gene set analysis. CoGAPS improves on other enrichment measurement methods by combining a Markov chain Monte Carlo (MCMC) matrix factorization algorithm (GAPS) with a threshold-independent statistic inferring activity on gene sets.

## Who should use CoGAPS?

Anyone can use CoGAPS; no machine learning experience is required.

## What kind of data does CoGAPS work on?

CoGAPS can be used to perform sparse matrix factorization on any data. And when this data represents biomolecules, to do gene set analysis.

## How do I cite CoGAPS?

If you use the CoGAPS package for your analysis, please cite:

Fertig EJ, Ding J, Favorov AV, Parmigiani G, Ochs MF (2010). “CoGAPS: an integrated R/C++ package to identify overlapping patterns of activation of biological processes from expression data.” <em>Bioinformatics</em>, **26**(21), 2792–2793.

If you use the gene set statistic, please cite Ochs et al. (2009)

### References

1. <a href="http://dx.doi.org/10.1073/pnas.0308531101" target="_blank">Brunet, J.-P., -P. Brunet, J., Tamayo, P., Golub, T. R. & Mesirov, J. P. Metagenes and molecular pattern discovery using matrix factorization. <em>Proceedings of the National Academy of Sciences</em> vol. 101 4164–4169 Preprint at https://doi.org/10.1073/pnas.0308531101 (2004).</a>
  
2. <a href="http://paperpile.com/b/NzqCvA/mt9uq" target="_blank">Moloshok, T. D. <em>et al.</em> Application of Bayesian decomposition for analysing microarray data. <em>Bioinformatics</em> <strong>18</strong>, 566–575 (2002).</a>

3. <a href="http://paperpile.com/b/NzqCvA/9Zr3" target="_blank">Stein-O’Brien, G. L. <em>et al.</em> Decomposing Cell Identity for Transfer Learning across Cellular Measurements, Platforms, Tissues, and Species. <em>Cell Syst</em> <strong>8</strong>, 395–411.e8 (2019).</a>
  
4. <a href="http://paperpile.com/b/NzqCvA/A7az" target="_blank">Clark, B. S. <em>et al.</em> Single-Cell RNA-Seq Analysis of Retinal Development Identifies NFI Factors as Regulating Mitotic Exit and Late-Born Cell Specification. <em>Neuron</em> <strong>102</strong>, 1111–1126.e5 (2019).</a>

5. <a href="http://paperpile.com/b/NzqCvA/WOzUm" target="_blank">Lê Cao, K.-A. <em>et al.</em> Community-wide hackathons to identify central themes in single-cell multi-omics. <em>Genome Biol.</em> <strong>22</strong>, 220 (2021).</a>

6. <a href="http://paperpile.com/b/NzqCvA/kHE7E" target="_blank">Zhu, X., Ching, T., Pan, X., Weissman, S. M. & Garmire, L. Detecting heterogeneity in single-cell RNA-Seq data by non-negative matrix factorization. <em>PeerJ</em> <strong>5</strong>, e2888 (2017).</a>

7. <a href="http://paperpile.com/b/NzqCvA/F5zYF" target="_blank">Duren, Z. <em>et al.</em> Integrative analysis of single-cell genomics data by coupled nonnegative matrix factorizations. <em>Proc. Natl. Acad. Sci. U. S. A.</em> <strong>115</strong>, 7723–7728 (2018).</a>

8. <a href="http://dx.doi.org/10.1101/2021.09.01.458620" target="_blank">DeBruine, Z. J., Melcher, K. & Triche, T. J. Fast and robust non-negative matrix factorization for single-cell experiments. <em>bioRxiv</em> 2021.09.01.458620 (2021) doi:10.1101/2021.09.01.458620.</a>

9. <a href="http://paperpile.com/b/NzqCvA/6391m" target="_blank">Cleary, B., Cong, L., Cheung, A., Lander, E. S. & Regev, A. Efficient Generation of Transcriptomic Profiles by Random Composite Measurements. <em>Cell</em> <strong>171</strong>, 1424–1436.e18 (2017).</a>

10. <a href="http://paperpile.com/b/NzqCvA/eb3to" target="_blank">Wu, Y., Tamayo, P. & Zhang, K. Visualizing and Interpreting Single-Cell Gene Expression Datasets with Similarity Weighted Nonnegative Embedding. <em>Cell Syst</em> <strong>7</strong>, 656–666.e4 (2018).</a>
