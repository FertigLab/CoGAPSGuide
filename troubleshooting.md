---

hero_image: /jubilant-bassoon/images/hero.jpg
<!-- hero_height: is-fullwidth -->
hero_darken: true

---

# Troubleshooting

## Procedure 1A: PyCoGAPS

| **Step** | **Problem**                                                                                                                                                                                                              | **Possible Reason**                                                                                               | **Solution**                                                                                                                                 |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| 1        | **Error with cloning repository due to large files (inputdata.h5ad, cogapsresult.h5ad)**                                                                                                                                 | Git LFS (large file storage) is not installed.                                                                    | Run the following command:  brew install git-lfs                                                                                             |
| 2        | **No module named pybind11**                                                                                                                                                                                             | pybind11 was not successfully installed                                                                           | If using conda, run: conda install -c conda-forge pybind11 Otherwise, run: pip install pybind11                                              |
| 2        | **src/bindings.cpp:1:10: fatal error: 'CoGAPS/src/GapsRunner.h' file not found** #include "CoGAPS/src/GapsRunner.h"          ^~~~~~~~~~~~~~~~~~~~~~~~~ 1 error generated. error: command 'gcc' failed with exit status 1 | CoGAPS library was not downloaded                                                                                 | Make sure you use --recursive flag when installing pycogaps.  git clone https://github.com/FertigLab/pycogaps.git --recursive                |
| 11       | Runtime is prohibitively long, given reasonable scales of data (typical timing is as given in n*log(n)).                                                                                                                 | If run times are prohibitive within reasonable scales of data, this may result from algorithm overfitting zeros.  | We recommend filtering the data only to genes that are reasonably expressed or filtering to a limited subset of genes (e.g., high variance). |
