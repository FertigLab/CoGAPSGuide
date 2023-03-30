---

hero_image: /CoGAPS/images/hero.jpg
<!-- hero_height: is-fullwidth -->
hero_darken: true
subtitle: User startup guide for the web-based CoGAPS API
toc: true

---

# GenePattern Notebook

## Notebook Setup

<strong>Timing: 5 min</strong>

1 . Log in to the <strong>GenePattern Notebook</strong> workspace, <a href="http://notebook.genepattern.org" target="_blank">notebook.genepattern.org</a>. If you do not have an account, click the "<strong>Register a new GenePattern Account</strong>" button, provide the registration information, and **log in**. Registration for GenePattern Notebook is free.

2 . Scroll to “<strong>Public Library</strong>.” You will see a list of available public project notebooks.

3 . In the “<strong>Search Library</strong>” box, search “<strong>PyCoGAPS</strong>.”

## Running PyCoGAPS on Simulated Toy Data

<strong>Timing: 8-10 min</strong>

4 . Select the “<strong>Single-Cell Workflow with PyCoGAPS</strong>” project notebook by clicking anywhere in its description and selecting “<strong>Run Notebook</strong>”. A copy of the project notebook will be saved in your account.

5 . Open the file called “<strong>Single-cell Analysis with PyCoGAPS.ipynb</strong>” which describes each step in this protocol and contains cells that will allow you to input datasets and set parameters. In the first cell, <strong>log in to your account</strong>.

6 . Follow the instructions in each blue panel, providing information where requested. You will need to input the “<strong>input_file</strong>” parameter, which in this simulated toy data case, is the “<strong>ModSimData.txt</strong>” file in the project folder. “<strong>num patterns</strong>” and “<strong>num iterations</strong>” are the most important parameters, but all parameter descriptions can be explored in the cell, or in <a href="/CoGAPS/procedurethree/#table-2">Table 2</a> for guidance on setting these and other key parameters. Click run once you have set desired parameters. 

Please note that once a run has been submitted, the status in the cell will change from “Pending” to “Running” to “Completed.” 

<strong><a href="/CoGAPS/troubleshooting/#procedure-3" target="_blank">TROUBLESHOOTING</a></strong>

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

### Table 2

|                       |                                       **Key parameters for CoGAPS/PyCoGAPS and guidance on setting their values**                                       |                                                                                                                                                                                                                                                                                                                                                                 |
|-----------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------:|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Parameter**         | **Description**                                                                                                                                         | **Guide to Setting**                                                                                                                                                                                                                                                                                                                                            |
| path                  | Path to data.                                                                                                                                           | Make sure data is log-normalized.                                                                                                                                                                                                                                                                                                                               |
| result_file           | Name of result .h5ad file to output.                                                                                                                    | Give this a descriptive name based on your data and run, such as PDACresult_50kiterations.h5ad                                                                                                                                                                                                                                                                  |
|                       |                                                                  _Standard Parameters_                                                                  |                                                                                                                                                                                                                                                                                                                                                                 |
| nPatterns             | Number of patterns CoGAPS will learn.                                                                                                                   | The optimal number of patterns to learn will vary based on your data and may require several runs of varying values to observe learned features. We recommend starting off with selecting a value that represents the number of experimental conditions, cell types, and/or biological processes expected from your data, as well as technical batches present. |
| nIterations           | Number of iterations of each phase of the algorithm.                                                                                                    | Higher iterations (ie. 50,000 iterations) is recommended as it will lead to better convergence. However, higher iterations greatly increases runtime, so we invite the user to play around with values to observe the tradeoff and determine the appropriate value.                                                                                             |
| useSparseOptimization | Speeds up performance with sparse data.                                                                                                                 | Set to true if using sparse data, ie. if roughly >80% of data is zero.                                                                                                                                                                                                                                                                                          |
|                       |                                                                     _Run Parameters_                                                                    |                                                                                                                                                                                                                                                                                                                                                                 |
| nThreads              | Maximum number of threads to run on.  Allows the underlying algorithm to run on multiple threads and has no effect on the mathematics of the algorithm. | The precise number of threads to use depends on many factors such as hardware and data size. The best approach is to play around with different values and see how it affects the estimated time.                                                                                                                                                               |
| transposeData         | Whether to transpose data.                                                                                                                              | Set to true if data is stored as samples x genes format (CoGAPS defaults to genes x samples format).                                                                                                                                                                                                                                                            |
|                       |                                                                 _Distributed Parameters_                                                                |                                                                                                                                                                                                                                                                                                                                                                 |
| distributed           | Whether to run distributed.                                                                                                                             | Recommended in most cases. Set to “genome-wide” for parallelization across genes, or “single-cell” for parallelization across cells.                                                                                                                                                                                                                            |
| nSets                 | Number of sets to break data into.                                                                                                                      | For distributed with “genome-wide”, do not set value to below 2,000 genes per set. For distributed with “single-cell”, make sure this value captures sufficient representation of all cell types in the data.                                                                                                                                                   |
| minNS                 | Minimum number of individual set contributions a cluster must contain.                                                                                  | Be cautious in setting this value too high as increasing robustness may also cause misses in rare phenomenon or cells.                                                                                                                                                                                                                                          |
| maxNS                 | Maximum number of individual set contributions a cluster can contain.                                                                                   | Modifying this parameter is only important for highly correlated processes.                                                                                                                                                                                                                                                                                     |
