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

____

To download PyCoGAPS without the large files (inputresult.h5ad and cogapsresult.h5ad), run the following command:

```yml
GIT_LFS_SKIP_SMUDGE=1 git clone https://github.com/FertigLab/pycogaps.git --recursive
```

Please note that if you would like to use the files (inputresult.h5ad and cogapsresulth5ad) later, you may download them from the repository as described in the Data section.

____

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

____

Install Anaconda from here: <a href="https://docs.anaconda.com/anaconda/install/" target="_blank">docs.anaconda.com/anaconda/install/</a>

Instructions for setting up a conda environment can be found here: <a href="https://conda.io/projects/conda/en/latest/user-guide/getting-started.html" target="_blank">conda.io/projects/conda/en/latest/user-guide/getting-started.html</a>

We recommend the user create a conda environment called ‘pycogaps’ and install all requirements and run code from within here.

____

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
