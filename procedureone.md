---

hero_image: /jubilant-bassoon/images/hero.jpg
<!-- hero_height: is-fullwidth -->
hero_darken: true

---

# Procedure 1: Running PyCoGAPS -- User startup guide for the Python CoGAPS API

We provide two options for running PyCoGAPS (Options A and B). Option A demonstrates running PyCoGAPS as a package in a Python script with an IDE, and Option B demonstrates automatic deployment and running NMF using a Docker image. Both options are functionally equivalent, so the user’s choice of interface should depend on factors such as familiarity with Python and desire for flexibility and modification. Option A provides a full walkthrough of PyCoGAPS package functions. However, to deploy and run PyCoGAPS in fewer steps with limited flexibility, we recommend following Option B. Please refer to Fig. 4 and/or Table 1 to determine which option is most appropriate to follow. 

## Option A

### Software Setup

<strong>Timing: 5-10 min</strong>

1.To download PyCoGAPS from GitHub with all data included (~2 GB memory), please run the following command, otherwise to omit the data, please refer to Box 2:

git clone https://github.com/FertigLab/pycogaps.git --recursive

?Troubleshooting

<strong>Box 2</strong>

---

To download PyCoGAPS without the large files (inputresult.h5ad and cogapsresult.h5ad), run the following command:

```yml
GIT_LFS_SKIP_SMUDGE=1 git clone https://github.com/FertigLab/pycogaps.git --recursive
```

Please note that if you would like to use the files (inputresult.h5ad and cogapsresulth5ad) later, you may download them from the repository as described in the Data section.

---

Expected output:

```yml
Cloning into 'pycogaps'...
remote: Enumerating objects: 1570, done.
remote: Counting objects: 100% (290/290), done.
remote: Compressing objects: 100% (191/191), done.
remote: Total 1570 (delta 160), reused 154 (delta 97), pack-reused 1280
Receiving objects: 100% (1570/1570), 8.97 MiB | 15.06 MiB/s, done.
Resolving deltas: 100% (950/950), done.
Filtering content: 100% (4/4), 2.29 GiB | 21.49 MiB/s, done.
Submodule 'src/CoGAPS' (https://github.com/FertigLab/CoGAPS.git) registered for path 'src/CoGAPS'
Cloning into '/Users/fertiglab/pycogaps/src/CoGAPS'...
remote: Enumerating objects: 16976, done.        
remote: Counting objects: 100% (343/343), done.        
remote: Compressing objects: 100% (156/156), done.        
remote: Total 16976 (delta 201), reused 312 (delta 187), pack-reused 16633        
Receiving objects: 100% (16976/16976), 177.58 MiB | 6.10 MiB/s, done.
Resolving deltas: 100% (10621/10621), done.
Submodule path 'src/CoGAPS': checked out 'e1e002caa009866d41402f3aa5ad3f97b541d962'
```

2. Install the required package dependencies with the following command. We recommend installing these dependencies in an Anaconda<sup>2</sup> environment(Box 3):

```yml
cd pycogaps
pip install -r requirements.txt
```

<strong>Box 3: Anaconda Environment</strong>

---

Install Anaconda from here: <a href="https://docs.anaconda.com/anaconda/install/" target="_blank">docs.anaconda.com/anaconda/install/</a>

Instructions for setting up a conda environment can be found here: <a href="https://conda.io/projects/conda/en/latest/user-guide/getting-started.html" target="_blank">conda.io/projects/conda/en/latest/user-guide/getting-started.html</a>

We recommend the user create a conda environment called ‘pycogaps’ and install all requirements and run code from within here.

---

?Troubleshooting

Now run the setup script. This installs the C++ core CoGAPS library.

```yml
python3 setup.py install
```

When PyCoGAPS has installed and built correctly, you should see this message, indicating PyCoGAPS is ready to use:

```yml
Finished processing dependencies for pycogaps==0.0.1
```

?Troubleshooting

### Running PyCoGAPS

<strong>[this code can be found in the reference file modsimvignette.py]</strong>

<strong>Timing: 3-5 min</strong>

To ensure PyCoGAPS is running properly on your computer, we will first perform a setup and run on a small, simulated toy dataset (single-cell data analysis will begin in Step 7). 

3. Import libraries. In your python script (file ending in .py), import the PyCoGAPS functions with the following lines:

```yml
from PyCoGAPS.parameters import *
from PyCoGAPS.pycogaps_main import CoGAPS
import scanpy as sc
```

4. Load sample data from directory.

```yml
modsimpath = "data/ModSimData.txt"
modsim = sc.read_text(modsimpath)
```

Examining the new modsim object in the python console, we see it is an Anndata object of dimension 25 x 20. 

```yml
modsim
AnnData object with n_obs × n_vars = 25 × 20
```

5. Next, we will set the parameters to be used by PyCoGAPS. First, we will create a CoParams object, then set parameters with the setParams function. 

```yml
params = CoParams(path=modsimpath)
params.printParams()
```

printParams() displays all parameters currently set for the parameter object. Since we just generated this object using the constructor, all default parameters are currently set.

```yml
-- Standard Parameters --
nPatterns:  3
nIterations:  1000
seed:  0
sparseOptimization:  False
-- Sparsity Parameters --
alpha: 0.01
maxGibbsMass:  100.0
```

Since we want to simulate a full-length run on this very small matrix, we need to change nIterations. Many parameters can be changed at once using this dictionary syntax:

```yml
setParams(params, {
    'nIterations': 50000,
    'seed': 42,
    'nPatterns': 3
})
```

For now, we will only modify the ‘nIterations’, ‘seed’, and ‘nPatterns’ parameters. 
Setting the seed fixes the random number generator so that the stochastic, MCMC algorithm used to solve for the A and P matrices in CoGAPS provides identical solutions between runs. More description of the parameters and parameter tuning can be found in Table 2. 

Verify nIterations was updated as anticipated:

```yml
>> params.printParams()

-- Standard Parameters --
nPatterns:  3
nIterations:  50000
seed:  42
sparseOptimization:  False
-- Sparsity Parameters --
alpha: 0.01
maxGibbsMass:  100.0
```

6. Since our parameters and data are now ready, we can start our PyCoGAPS run. As a best practice, we recommend always timing CoGAPS runs for your own records.

```yml
start = time.time()
modsimresult = CoGAPS(modsim, params)
print("TIME:", end - start)
```

Since modsim is a small, toy dataset, the expected runtime is only about 3 seconds. Verify that the following output appears:

```yml
This is pycogaps version  0.0.1

Running Standard CoGAPS on provided data object ( 25 genes and 20 samples) with parameters: 


-- Standard Parameters --
nPatterns:  3
nIterations:  50000
seed:  42
sparseOptimization:  False
-- Sparsity Parameters --
alpha: 0.01
maxGibbsMass:  100.0
Data Model: Dense, Normal
Sampler Type: Sequential
Loading Data...Done! (00:00:00)
-- Equilibration Phase --
1000 of 50000, Atoms: 41(A), 37(P), ChiSq: 3076, Time: 00:00:00 / 00:00:00
2000 of 50000, Atoms: 51(A), 39(P), ChiSq: 1764, Time: 00:00:00 / 00:00:00
3000 of 50000, Atoms: 53(A), 41(P), ChiSq: 892, Time: 00:00:00 / 00:00:00
4000 of 50000, Atoms: 50(A), 42(P), ChiSq: 695, Time: 00:00:00 / 00:00:00
5000 of 50000, Atoms: 52(A), 44(P), ChiSq: 519, Time: 00:00:00 / 00:00:00
[ … ]
45000 of 50000, Atoms: 72(A), 51(P), ChiSq: 107, Time: 00:00:00 / 00:00:00
46000 of 50000, Atoms: 78(A), 52(P), ChiSq: 128, Time: 00:00:00 / 00:00:00
47000 of 50000, Atoms: 79(A), 48(P), ChiSq: 95, Time: 00:00:00 / 00:00:00
48000 of 50000, Atoms: 71(A), 56(P), ChiSq: 136, Time: 00:00:00 / 00:00:00
49000 of 50000, Atoms: 72(A), 47(P), ChiSq: 143, Time: 00:00:00 / 00:00:00
50000 of 50000, Atoms: 69(A), 53(P), ChiSq: 131, Time: 00:00:00 / 00:00:00
-- Sampling Phase --
1000 of 50000, Atoms: 74(A), 55(P), ChiSq: 104, Time: 00:00:00 / 00:00:00
2000 of 50000, Atoms: 75(A), 55(P), ChiSq: 123, Time: 00:00:00 / 00:00:00
3000 of 50000, Atoms: 87(A), 49(P), ChiSq: 101, Time: 00:00:00 / 00:00:00
4000 of 50000, Atoms: 82(A), 47(P), ChiSq: 102, Time: 00:00:00 / 00:00:00
5000 of 50000, Atoms: 82(A), 44(P), ChiSq: 100, Time: 00:00:00 / 00:00:00
[ … ]
45000 of 50000, Atoms: 71(A), 52(P), ChiSq: 132, Time: 00:00:01 / 00:00:01
46000 of 50000, Atoms: 68(A), 50(P), ChiSq: 130, Time: 00:00:01 / 00:00:01
47000 of 50000, Atoms: 75(A), 51(P), ChiSq: 140, Time: 00:00:01 / 00:00:01
48000 of 50000, Atoms: 74(A), 51(P), ChiSq: 108, Time: 00:00:01 / 00:00:01
49000 of 50000, Atoms: 74(A), 52(P), ChiSq: 108, Time: 00:00:01 / 00:00:01
50000 of 50000, Atoms: 81(A), 47(P), ChiSq: 108, Time: 00:00:01 / 00:00:01

GapsResult result object with 25 features and 20 samples
3 patterns were learned
```

Now we’ll take a quick look at the result object, to make sure there are two resulting base matrices filled with plausible values.

```yml
>> modsimresult
AnnData object with n_obs × n_vars = 25 × 20
    obs: 'Pattern1', 'Pattern2', 'Pattern3'
    var: 'Pattern1', 'Pattern2', 'Pattern3'
    uns: 'asd', 'psd', 'atomhistoryA', 'atomhistoryP', 'averageQueueLengthA', 'averageQueueLengthP', 'chisqHistory', 'equilibrationSnapshotsA', 'equilibrationSnapshotsP', 'meanChiSq', 'meanPatternAssignment', 'pumpMatrix', 'samplingSnapshotsA', 'samplingSnapshotsP', 'seed', 'totalRunningTime', 'totalUpdates'

>> modsimresult.obs.head()

    Pattern1  Pattern2  Pattern3
0  11.975077  0.101262  0.419482
1  10.741890  0.125388  1.356528
2   8.950110  0.035884  2.792770
3   7.521177  0.019195  3.895204
4   6.137812  0.014312  4.937158

>> modsimresult.var.head()

   Pattern1  Pattern2  Pattern3
0  0.001125  0.000760  0.013232
1  0.075658  0.000514  0.135343
2  0.341718  0.002400  0.604787
3  0.567491  0.004287  1.000000
4  0.391151  0.002598  0.640158
```

This indicates that PyCoGAPS has been set up and run correctly, and we can now proceed to analyzing experimental single-cell data.
