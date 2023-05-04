---

hero_image: /CoGAPS/images/hero.jpg
<!-- hero_height: is-fullwidth -->
hero_darken: true

---

# FAQ

## What is NMF?

NMF (Nonnegative Matrix Factorization) is a mathematical technique with a long history in the field of genomics for the analysis of bulk RNA sequencing data<sup>1,2</sup>, and it has been widely adopted as a powerful dimensionality reduction tool for single-cell data as well<sup>3,4,5–10</sup>. It is unique among matrix factorization methods in identifying overlapping patterns in high-throughput data to define biological processes that can co-occur across cell types or biological conditions<sup>11</sup>.

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
  
2. <a href="https://www.researchgate.net/publication/11355743_Application_of_Bayesian_Decomposition_for_analysing_microarray_data" target="_blank">Moloshok, T. D. <em>et al.</em> Application of Bayesian decomposition for analysing microarray data. <em>Bioinformatics</em> <strong>18</strong>, 566–575 (2002).</a>

3. <a href="https://www.biorxiv.org/content/10.1101/395004v2" target="_blank">Stein-O’Brien, G. L. <em>et al.</em> Decomposing Cell Identity for Transfer Learning across Cellular Measurements, Platforms, Tissues, and Species. <em>Cell Syst</em> <strong>8</strong>, 395–411.e8 (2019).</a>
  
4. <a href="https://www.researchgate.net/publication/333299631_Single-Cell_RNA-Seq_Analysis_of_Retinal_Development_Identifies_NFI_Factors_as_Regulating_Mitotic_Exit_and_Late-Born_Cell_Specification" target="_blank">Clark, B. S. <em>et al.</em> Single-Cell RNA-Seq Analysis of Retinal Development Identifies NFI Factors as Regulating Mitotic Exit and Late-Born Cell Specification. <em>Neuron</em> <strong>102</strong>, 1111–1126.e5 (2019).</a>

5. <a href="https://genomebiology.biomedcentral.com/articles/10.1186/s13059-021-02433-9" target="_blank">Lê Cao, K.-A. <em>et al.</em> Community-wide hackathons to identify central themes in single-cell multi-omics. <em>Genome Biol.</em> <strong>22</strong>, 220 (2021).</a>

6. <a href="https://peerj.com/articles/2888/" target="_blank">Zhu, X., Ching, T., Pan, X., Weissman, S. M. & Garmire, L. Detecting heterogeneity in single-cell RNA-Seq data by non-negative matrix factorization. <em>PeerJ</em> <strong>5</strong>, e2888 (2017).</a>

7. <a href="https://www.biorxiv.org/content/10.1101/312348v1.full" target="_blank">Duren, Z. <em>et al.</em> Integrative analysis of single-cell genomics data by coupled nonnegative matrix factorizations. <em>Proc. Natl. Acad. Sci. U. S. A.</em> <strong>115</strong>, 7723–7728 (2018).</a>

8. <a href="https://www.biorxiv.org/content/10.1101/2021.09.01.458620v1" target="_blank">DeBruine, Z. J., Melcher, K. & Triche, T. J. Fast and robust non-negative matrix factorization for single-cell experiments. <em>bioRxiv</em> 2021.09.01.458620 (2021) doi:10.1101/2021.09.01.458620.</a>

9. <a href="https://www.researchgate.net/publication/321113502_Efficient_Generation_of_Transcriptomic_Profiles_by_Random_Composite_Measurements" target="_blank">Cleary, B., Cong, L., Cheung, A., Lander, E. S. & Regev, A. Efficient Generation of Transcriptomic Profiles by Random Composite Measurements. <em>Cell</em> <strong>171</strong>, 1424–1436.e18 (2017).</a>

10. <a href="https://www.biorxiv.org/content/10.1101/276261v5" target="_blank">Wu, Y., Tamayo, P. & Zhang, K. Visualizing and Interpreting Single-Cell Gene Expression Datasets with Similarity Weighted Nonnegative Embedding. <em>Cell Syst</em> <strong>7</strong>, 656–666.e4 (2018).</a>

11. <a href="https://www.cell.com/trends/genetics/fulltext/S0168-9525(18)30124-0" target="_blank">Stein-O’Brien, G. L. <em>et al.</em> Enter the Matrix: Factorization Uncovers Knowledge from Omics. <em>Trends Genet</em>. <strong>34</strong>, 790–805 (2018).</a>
