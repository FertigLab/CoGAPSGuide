---

hero_image: /jubilant-bassoon/images/hero.jpg
<!-- hero_height: is-fullwidth -->
hero_darken: true

---

## Procedures

We provide three independent procedures (Procedure 1-3) for NMF analysis. Procedure 1 demonstrates PyCoGAPS, Procedure 2 demonstrates CoGAPS, and Procedure 3 demonstrates GenePattern Notebook. All of these procedures are functionally equivalent and share the same CoGAPS backend, so the user’s choice of interface should depend on factors such as computing performance, familiarity with the programming language, and programming expertise. Please refer to Fig. 4 and/or Table 1 to determine which procedure is most appropriate to follow. 

Additionally, each procedure instructs the user to conduct a run on a simulated, small toy dataset called ModSim to quickly ensure proper setup of the package and environment. Then, each procedure demonstrates running and analysis on a larger scRNA-seq PDAC dataset to draw biological conclusions. Fig. 5 provides a general procedure workflow overview for running each procedure.

## Data

All three procedures are demonstrated with publicly available data which we have pre-processed and provided alongside the code for convenience. All necessary data files to run the vignette are automatically included in both R and Python application programming interfaces (APIs). 

ModSim is a small simulated dataset that will be used to ensure proper setup and run of PyCoGAPS/CoGAPS in each procedure. 

The single-cell protocol is demonstrated using preprocessed and harmonized scRNAseq data of 25,422 pancreatic epithelial cells from two studies of pancreatic ductal adenocarcinoma. In the python vignette this is retrieved from inputdata.h5ad, and in R it can be loaded as a Seurat object from inputdata.Rds. We note that this is the same data in two different formats necessitated by the different languages of the APIs.

<ul>
  <li>(Required) ModSim simulated dataset and a reference NMF result live in CoGAPS/pycogaps github repositories in the data/ directories.
  <ul>
    <li>Name: ModSimData.txt (25 “genes” x 20 “cells”, simulated data)</li>
    <li>Reference result: ModSimResult.h5ad (anndata result object)</li>
    </ul>
    </ul>

  <ul>
  <li>(Optional) scRNA-seq PDAC dataset</li>
<ul>
  <li>We encourage the user to start with the annotated and prepared .h5ad file available in the github repositories in the data/ directory.</li>
<li>Reference dataset: inputdata.h5ad (Python) inputdata.Rds (R) (dimension: 15219 genes × 25422 cells, size: 1GB)</li>
<li>Reference result: cogapsresult.h5ad (Python) cogapsresult.Rds (R) (dimension: 15219 genes × 25422 cells, objects size: 1GB)</li>
  </ul>
</ul>

All code and data needed to reproduce the results of these workflows can also be found hosted on Zenodo<sup>1</sup> at <a href="https://zenodo.org/record/7709664" target="_blank">zenodo.org/record/7709664</a>

### References

1. <em>zenodo: Research. Shared.</em> (Github).
