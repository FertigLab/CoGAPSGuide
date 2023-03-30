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

<p style="margin-left: 25px;">
<strong><a href="/CoGAPS/troubleshooting/#procedure-3" target="_blank">TROUBLESHOOTING</a></strong>
</p>
  
7 . As described in the notebook instructions, please make sure to save the result file locally first, then re-upload it to the project notebook. 

## Running PyCoGAPS on Single Cell Data

<strong>Timing: 5 min - 2 days (depending on whether user runs NMF or uses precomputed result)</strong>

8 . Click the ‘+’ button of the PyCoGAPS cell to display the parameter inputs again. You may reset the parameters by selecting the settings icon. To run PyCoGAPS, on the provided PDAC dataset, the link to the file can be found here and directly passed into the ‘input_file’ cell (there is no need to download the data and re-upload it to the project folder): <a href="https://datasets.genepattern.org/?prefix=data/module_support_files/PyCoGAPS/inputdata.h5ad" target="_blank">datasets.genepattern.org/?prefix=data/module_support_files/PyCoGAPS/inputdata.h5ad</a>.

9 . Once desired parameters have been set, run the cell to submit the job.

<strong>Analyzing the PyCoGAPS Result</strong>

<strong>Timing 20-30 min</strong>

10 . Follow and run the cells to perform analysis of your output PyCoGAPS results. These cells will call the various functions described in other procedures of this manuscript to allow you to visualize and interpret your data.

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
