---

hero_image: /CoGAPS/images/hero.jpg
<!-- hero_height: is-fullwidth -->
hero_darken: true

---

# Procedure 3: Running GenePattern Notebook — User startup guide for the web-based CoGAPS API

## Notebook Setup

<strong>Timing: 5 min</strong>

1 . Log in to the GenePattern Notebook workspace, <a href="http://notebook.genepattern.org" target="_blank">notebook.genepattern.org</a>. If you do not have an account, click the “Register a new GenePattern Account” button, provide the registration information, and log in. Registration for GenePattern Notebook is free.

2 . Scroll to “Public Library.” You will see a list of available public project notebooks.

3 . In the “Search Library” box, search “PyCoGAPS.”

## Running PyCoGAPS on Simulated Toy Data

<strong>Timing: 8-10 min</strong>

4 . Select the “Single-Cell Workflow with PyCoGAPS” project notebook by clicking anywhere in its description and selecting “Run Notebook”. A copy of the project notebook will be saved in your account.

5 . Open the file called “Single-cell Analysis with PyCoGAPS.ipynb” which describes each step in this protocol and contains cells that will allow you to input datasets and set parameters. In the first cell, log in to your account.

6 . Follow the instructions in each blue panel, providing information where requested. You will need to input the “input_file” parameter, which in this simulated toy data case, is the “ModSimData.txt” file in the project folder. “num patterns” and “num iterations” are the most important parameters, but all parameter descriptions can be explored in the cell, or in Table 2 for guidance on setting these and other key parameters. Click run once you have set desired parameters. 

Please note that once a run has been submitted, the status in the cell will change from “Pending” to “Running” to “Completed.” 

?Troubleshooting 

7 . As described in the notebook instructions, please make sure to save the result file locally first, then re-upload it to the project notebook. 

## Running PyCoGAPS on Single Cell Data

<strong>Timing: 5 min - 2 days (depending on whether user runs NMF or uses precomputed result)</strong>

8 . Click the ‘+’ button of the PyCoGAPS cell to display the parameter inputs again. You may reset the parameters by selecting the settings icon. To run PyCoGAPS, on the provided PDAC dataset, the link to the file can be found here and directly passed into the ‘input_file’ cell (there is no need to download the data and re-upload it to the project folder): https://datasets.genepattern.org/?prefix=data/module_support_files/PyCoGAPS/inputdata.h5ad.

9 . Once desired parameters have been set, run the cell to submit the job.

<strong>Analyzing the PyCoGAPS Result

Timing 20-30 min</strong>

10 . Follow and run the cells to perform analysis of your output PyCoGAPS results. These cells will call the various functions described in other procedures of this manuscript to allow you to visualize and interpret your data.

## Anticipated Results

The output you should obtain from a PyCoGAPS run (Procedure 1A/B or Procedure 3) is an anndata object, stored as an .h5ad file. In the anndata object, the lower dimensional representation of the samples (P matrix) is stored in the .var slot and the weight of the features (A matrix) is stored in the .obs slot. For an m by p dimension gene expression input, the P matrix or .var slot should have dimension m by k, and the A matrix or .obs slot should have dimension k by p, where k is the number of patterns.

Further metrics are stored in the .uns slot of the result object. This includes standard deviations across the sample points for both the P and A matrix stored in “psd” and “asd” respectively, the mean chi squared value stored in “meanchisq”, the total running time stored in “totalRunningTime” and more. An example output including all metadata can be found in Box 18.

---

<strong>Box 18: PyCoGAPS Anndata Result & Metadata</strong>

```yml
AnnData object with n_obs × n_vars = 15219 × 25442
    obs: 'Pattern1', 'Pattern2', 'Pattern3', 'Pattern4', 'Pattern5', 'Pattern6', 'Pattern7', 'Pattern8'
    var: 'Pattern1', 'Pattern2', 'Pattern3', 'Pattern4', 'Pattern5', 'Pattern6', 'Pattern7', 'Pattern8'
    uns: 'asd', 'atomhistoryA', 'atomhistoryP', 'averageQueueLengthA', 'averageQueueLengthP', 'chisqHistory', 'equilibrationSnapshotsA', 'equilibrationSnapshotsP', 'meanChiSq', 'meanPatternAssignment', 'psd', 'pumpMatrix', 'samplingSnapshotsA', 'samplingSnapshotsP', 'seed', 'totalRunningTime', 'totalUpdates'
    varm: 'X_aligned', 'X_pca', 'X_umap'
```

---

The output you should obtain from a CoGAPS run (Procedure 2) is an .Rds file. In this object, the lower dimensional representation of the samples (P matrix) is stored in the “featureLoadings” slot and the weight of the features (A matrix) is stored in the “sampleFactors” slot. For an m by p dimension gene expression input, the P matrix should have dimension m by k, and the A matrix should have dimension k by p, where k is the number of patterns.

Standard deviation matrices are stored in the slots “factorStdDev” and “loadingStdDev” corresponding to sampleFactors and featureLoadings.

Additionally, metadata contains information for the run such as how it was parallelized stored in “subsets”, the mean ChiSq value during the run stored in “meanChiSq”, and the parameters used in the run stored in “params”. Other information may be present in the metadata depending on your run options shown in Box 19.


---

<strong>Box 19: CoGAPS Result & Metadata</strong>

```yml
> cogapsresult
[1] "CogapsResult object with 15176 features and 25442 samples"
[1] "8 patterns were learned"
```

![Box 19](images/box19.png)

```yml
> names(cogapsresult@metadata)
[1] "meanChiSq"         "firstPass"         "unmatchedPatterns" "clusteredPatterns"
[5] "CorrToMeanPattern" "subsets"           "params"            "version"          
[9] "logStreamName"
```

---

Once the result object is obtained, the user may follow the steps in any of the three procedures (Python, R, or GenePattern) in “Analyzing the PyCoGAPS/CoGAPS result” for interpretation.

Because CoGAPS uses MCMC sampling to find the values of the A and P matrices, the results are stochastic. While results will vary between simulations, we have observed that solutions from multiple runs tend to have qualitatively similar gene signatures and cell weights in permuted pattern order. For reproducibility of CoGAPS results, we recommend setting the seed for each run and saving CoGAPS results after completion of the run as an intermediate object prior to interpretation. 
