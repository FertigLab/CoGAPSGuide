---

hero_image: /CoGAPS/images/hero.jpg
<!-- hero_height: is-fullwidth -->
hero_darken: true
title: Docker
subtitle: User Startup Guide
toc: true

---

# Option B

<strong>Software Setup</strong>

<strong>Timing: 5 min</strong>

**1** . Pull the PyCoGAPS Docker container and set up the working directory.

For Mac users, **copy** the commands and **paste** in terminal:

```docker
docker pull fertiglab/pycogaps
mkdir PyCoGAPS
cd PyCoGAPS
curl -O https://raw.githubusercontent.com/FertigLab/pycogaps/master/params.yaml
mkdir data
cd data
curl -O https://raw.githubusercontent.com/FertigLab/pycogaps/master/data/ModSimData.txt
cd ..
```

For Windows (Ubuntu) users, **copy** the commands and **paste** in terminal:

```yml
docker pull fertiglab/pycogaps
mkdir PyCoGAPS
cd PyCoGAPS
curl.exe -o index.html https://raw.githubusercontent.com/FertigLab/pycogaps/master/params.yaml
mkdir data
cd data
curl.exe -o index.html https://raw.githubusercontent.com/FertigLab/pycogaps/master/data/GIST.csv
cd..
```

<p style="margin-left: 25px;">
<strong><a href="/CoGAPS/troubleshooting/#procedure-1b" target="_blank">TROUBLESHOOTING</a></strong>
</p>
       
## Running PyCoGAPS on Simulated Toy Data

<strong>Timing: 2 min</strong>

**2** . To ensure PyCoGAPS is running properly on your computer, we will first perform a setup and run on the ModSim dataset (running PyCoGAPS on the single-cell data will be performed later in [Step 3](/CoGAPS/optionb/#running-pycogaps-on-single-cell-data). The dataset has already been downloaded in Step 1. **Run the following commands** in terminal:

```yml
docker run -v $PWD:$PWD fertiglab/pycogaps $PWD/params.yaml
```

For users with an **M1 processing chip**, please add the following flag to the above command:

```yml
--platform linux/amd64
```

This produces a CoGAPS run on a simple dataset with default parameters. Please check that your output matches the expected in **Box 11**.

---

<strong>Box 11: Expected PyCoGAPS Docker Output</strong>

```yml
______      _____       _____   ___  ______  _____ 
| ___ \    /  __ \     |  __ \ / _ \ | ___ \/  ___|
| |_/ /   _| /  \/ ___ | |  \// /_\ \| |_/ /\ `--. 
|  __/ | | | |    / _ \| | __ |  _  ||  __/  `--. |
| |  | |_| | \__/\ (_) | |_\ \| | | || |    /\__/ /
\_|   \__, |\____/\___/ \____/\_| |_/\_|    \____/ 
       __/ |                                       
      |___/ 
   
   
pycogaps version  0.0.1
This vignette was built using pycogaps version 0.0.1

This is pycogaps version  0.0.1
Running Standard CoGAPS on ModSimData.txt ( 25 genes and 20 samples) with parameters: 

-- Standard Parameters --
nPatterns:  3
nIterations:  1000
seed:  0
sparseOptimization:  False


-- Sparsity Parameters --
alpha: 0.01
maxGibbsMass:  100.0


Data Model: Dense, Normal
Sampler Type: Sequential
Loading Data...Done! (00:00:00)
-- Equilibration Phase --
1000 of 1000, Atoms: 70(A), 54(P), ChiSq: 1351, Time: 00:00:00 / 00:00:00
-- Sampling Phase --
1000 of 1000, Atoms: 78(A), 48(P), ChiSq: 1185, Time: 00:00:00 / 00:00:00

GapsResult result object with 25 features and 20 samples
3 patterns were learned

Pickling complete!
```

---

CoGAPS has successfully **completed running** and has **saved** the result file as **result.pkl** in a created **output/ folder**. Your working directory is the PyCoGAPS folder with the following structure and files, shown in **Box 12**.

---

<strong>Box 12: PyCoGAPS Working Directory</strong>

```yml
PyCoGAPS
├── data
│   └── ModSimData.txt
├── params.yaml
├── output
│   └── result.pkl
```
---

## Running PyCoGAPS on Single Cell Data

<strong>Timing: 5 min - 2 days (depending on whether user runs NMF or uses precomputed result)</strong>

**3** . Now that PyCoGAPS has been set up and run correctly, we can now proceed to analyzing experimental single-cell data. Navigate to the ‘**data**’ folder created earlier, and **run the following command**:

```yml
cd data
curl -O https://raw.githubusercontent.com/FertigLab/pycogaps/master/data/inputdata.h5ad
```

<strong>! CRITICAL -</strong> Always make sure to move the data you seek to analyze into the created ‘**data**’ folder. 

**4** . We will then modify the default parameters before running PyCoGAPS. All parameter values can be modified directly in the **params.yaml file** already downloaded earlier in **Step 1**.

We will do this by first opening **params.yaml** with any text or code editor. Then, **modify the following line to**:

```yml
path: ‘data/inputdata.h5ad’
```

Then, **modify** any additional desired parameters and **save the file** (**Box 13**). 

---

<strong>Box 13: Example snippet of params.yaml</strong>

The **params.yaml** file holds all parameters that can be inputted to PyCoGAPS. A snippet of **params.yaml** is shown below, where we have changed some default parameter values to our own specified example values.

```yml
## This file holds all parameters to be passed into PyCoGAPS.
## To modify default parameters, simply replace parameter values below with user-specified values, and save file. 

# RELATIVE path to data -- make sure to move your data into the created data/ folder
path: data/ModSimData.txt

# result output file name 
result_file: ModSimResult.h5ad

standard_params:
  # number of patterns CoGAPS will learn
  nPatterns: 10
  # number of iterations for each phase of the algorithm
  nIterations: 5000
  # random number generator seed
  seed: 0
  # speeds up performance with sparse data (roughly >80% of data is zero), note this can only be used with the default uncertainty
  useSparseOptimization: True
 
...
```

A complete list of input options and their descriptions can be found as comments in **params.yaml** and guide to setting key parameters in [Table 2](/CoGAPS/optionb/#table-2-key-parameters-for-cogapspycogaps-and-guidance-on-setting-their-values).

---

Note the ‘**distributed**’ parameter enables parallelization to decrease runtimes which we recommended for most cases. Please refer to **Box 14** for how to run distributed PyCoGAPS.

A description and guide for setting key PyCoGAPS parameters can be found in [Table 2](/CoGAPS/optionb/#table-2-key-parameters-for-cogapspycogaps-and-guidance-on-setting-their-values). There are many more additional parameters that can be set depending on your goals, which we invite the reader to explore in our **GitHub documentation**.

---

<strong>Box 14: Distributed PyCoGAPS in Docker</strong>

A snippet of ```params.yaml``` is shown below where ```distributed_params``` parameters are modified.

```yml
## This file holds all parameters to be passed into PyCoGAPS.
...

distributed_params:
  #  either null or genome-wide
  distributed: genome-wide
  # number of sets to break data into
  nSets: 4
  # number of branches at which to cut dendrogram used in pattern matching
  cut: null
  # minimum of individual set contributions a cluster must contain
  minNS: null
  # maximum of individual set contributions a cluster can contain
  maxNS: null
```

For Distributed PyCoGAPS, once all worker threads have started running their iterations, you will see periodic output like this:

```yml
1000 of 50000, Atoms: 5424(A), 21232(P), ChiSq: 138364000, Time: 00:03:47 / 11:13:32
1000 of 50000, Atoms: 5394(A), 20568(P), ChiSq: 133824536, Time: 00:03:46 / 11:10:34
1000 of 50000, Atoms: 5393(A), 21161(P), ChiSq: 133621048, Time: 00:03:51 / 11:25:24
1000 of 50000, Atoms: 5527(A), 22198(P), ChiSq: 137671296, Time: 00:04:00 / 11:52:06
1000 of 50000, Atoms: 5900(A), 20628(P), ChiSq: 137228688, Time: 00:03:58 / 11:46:10
```

---

**5** . Now that all parameters are set, we are ready to **run PyCoGAPS**. Please note that this is the most time-consuming step of the procedure. Timing can take several hours and scales nlog(n) based on dataset size (see **Timing** section below), as well as the parameter values set for ‘**nPatterns**’ and ‘**nIterations**’. Time is increased when learning more patterns, when running more iterations, and when running a larger dataset, with iterations having the largest variable impact on the runtime of the NMF function.

**Run PyCoGAPS** with the following command in terminal:

```yml
docker run -v $PWD:$PWD fertiglab/pycogaps $PWD/params.yaml
```

The result object will automatically save in the ‘**output**’ folder, with the name given by the ‘**result_file**’ parameter. 

<strong>! PAUSE POINT -</strong> Now we have successfully **generated** and **saved** a CoGAPS result. The procedure may be **paused**. The following steps will walk through **analyzing** and **visualizing** the generated saved result.

## Analyzing the PyCoGAPS Result

<strong>Timing: 20-30 min</strong>

**6** . **Download** the analysis functions and requirements files with the following command:

```yml
curl -O https://raw.githubusercontent.com/FertigLab/pycogaps/master/PyCoGAPS/analysis_functions.py
curl -O
https://raw.githubusercontent.com/FertigLab/pycogaps/master/PyCoGAPS/requirements_analysis.txt 
```

**7** . **Install** the analysis functions dependencies with the following command:

```yml
pip install -r analysis_requirements.txt
```

**8** . **Open** a new Python file (in any preferred IDE, see **Software** section above) and **include the following line**:

```yml
from analysis_functions import *
```

<p style="margin-left: 25px;">
<strong><a href="/CoGAPS/troubleshooting/#procedure-1b" target="_blank">TROUBLESHOOTING</a></strong>
</p>
       
Please **skip to the section above** titled, “<strong>Analyzing the PyCoGAPS Result</strong>” in <a href="/CoGAPS/optiona/#analyzing-the-pycogaps-result" target="_blank">Procedure 1 Option A Step 13</a> to continue following the analysis and visualization workflow. 


### Table 2: Key parameters for CoGAPS/PyCoGAPS and guidance on setting their values.

| **Parameter**         | **Description**                                                                                                                                         | **Guide to Setting**                                                                                                                                                                                                                                                                                                                                            |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| path                  | Path to data.                                                                                                                                           | Make sure data is log-normalized.                                                                                                                                                                                                                                                                                                                               |
| result_file           | Name of result .h5ad file to output.                                                                                                                    | Give this a descriptive name based on your data and run, such as PDACresult_50kiterations.h5ad                                                                                                                                                                                                                                                                  |
|                       |                                                                **_Standard Parameters_**                                                                |                                                                                                                                                                                                                                                                                                                                                                 |
| nPatterns             | Number of patterns CoGAPS will learn.                                                                                                                   | The optimal number of patterns to learn will vary based on your data and may require several runs of varying values to observe learned features. We recommend starting off with selecting a value that represents the number of experimental conditions, cell types, and/or biological processes expected from your data, as well as technical batches present. |
| nIterations           | Number of iterations of each phase of the algorithm.                                                                                                    | Higher iterations (ie. 50,000 iterations) is recommended as it will lead to better convergence. However, higher iterations greatly increases runtime, so we invite the user to play around with values to observe the tradeoff and determine the appropriate value.                                                                                             |
| useSparseOptimization | Speeds up performance with sparse data.                                                                                                                 | Set to true if using sparse data, ie. if roughly >80% of data is zero.                                                                                                                                                                                                                                                                                          |
|                       |                                                                   **_Run Parameters_**                                                                  |                                                                                                                                                                                                                                                                                                                                                                 |
| nThreads              | Maximum number of threads to run on.  Allows the underlying algorithm to run on multiple threads and has no effect on the mathematics of the algorithm. | The precise number of threads to use depends on many factors such as hardware and data size. The best approach is to play around with different values and see how it affects the estimated time.                                                                                                                                                               |
| transposeData         | Whether to transpose data.                                                                                                                              | Set to true if data is stored as samples x genes format (CoGAPS defaults to genes x samples format).                                                                                                                                                                                                                                                            |
|                       |                                                               **_Distributed Parameters_**                                                              |                                                                                                                                                                                                                                                                                                                                                                 |
| distributed           | Whether to run distributed.                                                                                                                             | Recommended in most cases. Set to “genome-wide” for parallelization across genes, or “single-cell” for parallelization across cells.                                                                                                                                                                                                                            |
| nSets                 | Number of sets to break data into.                                                                                                                      | For distributed with “genome-wide”, do not set value to below 2,000 genes per set. For distributed with “single-cell”, make sure this value captures sufficient representation of all cell types in the data.                                                                                                                                                   |
| minNS                 | Minimum number of individual set contributions a cluster must contain.                                                                                  | Be cautious in setting this value too high as increasing robustness may also cause misses in rare phenomenon or cells.                                                                                                                                                                                                                                          |
| maxNS                 | Maximum number of individual set contributions a cluster can contain.                                                                                   | Modifying this parameter is only important for highly correlated processes.                                                                                                                                                                                                                                                                                     |
