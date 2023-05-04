---

hero_image: /cogaps/images/hero.jpg
<!-- hero_height: is-fullwidth -->
hero_darken: true

---

# Troubleshooting

## Procedure 1A

### PyCoGAPS

| **Step** | **Problem**                                                                                                                                                                                                              | **Possible Reason**                                                                                               | **Solution**                                                                                                                                 |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| 1        | **Error with cloning repository due to large files (inputdata.h5ad, cogapsresult.h5ad)**                                                                                                                                 | Git LFS (large file storage) is not installed.                                                                    | Run the following command:  brew install git-lfs                                                                                             |
| 2        | **No module named pybind11**                                                                                                                                                                                             | pybind11 was not successfully installed                                                                           | If using conda, run: conda install -c conda-forge pybind11 Otherwise, run: pip install pybind11                                              |
| 2        | **src/bindings.cpp:1:10: fatal error: 'CoGAPS/src/GapsRunner.h' file not found** #include "CoGAPS/src/GapsRunner.h"          ^~~~~~~~~~~~~~~~~~~~~~~~~ 1 error generated. error: command 'gcc' failed with exit status 1 | CoGAPS library was not downloaded                                                                                 | Make sure you use --recursive flag when installing pycogaps.  git clone https://github.com/FertigLab/pycogaps.git --recursive                |
| 11       | Runtime is prohibitively long, given reasonable scales of data (typical timing is as given in n*log(n)).                                                                                                                 | If run times are prohibitive within reasonable scales of data, this may result from algorithm overfitting zeros.  | We recommend filtering the data only to genes that are reasonably expressed or filtering to a limited subset of genes (e.g., high variance). |

## Procedure 1B
### PyCoGAPS in Docker

| **Step** | **Problem**                                                                                       | **Possible Reason**                                                               | **Solution**                                                                                                  |
|----------|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| 1        | Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running? | Docker is not started up / running.                                               | Open the Docker application or run the following command:  docker run -d -p 80:80 docker/getting-started      |
| 8        | ModuleNotFoundError: No module named 'analysis_functions'                                         | analysis_functions.py file is not in the same directory as your new Python file.  | Make sure analysis_functions.py and your new Python file for calling the functions are in the same directory. |

## Procedure 2
### R CoGAPS

| **Step** | **Problem**                                                                                              | **Possible Reason**                                                                                               | **Solution**                                                                                                                                 |
|----------|----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| 8        | Runtime is prohibitively long, given reasonable scales of data (typical timing is as given in n*log(n)). | If run times are prohibitive within reasonable scales of data, this may result from algorithm overfitting zeros.  | We recommend filtering the data only to genes that are reasonably expressed or filtering to a limited subset of genes (e.g., high variance). |

## Procedure 3
### GenePattern Notebook

| **Step** | **Problem**                           | **Possible Reason**                       | **Solution**                                                                                  |
|----------|---------------------------------------|-------------------------------------------|-----------------------------------------------------------------------------------------------|
| Step 6   | FileNotFoundError                     | Data file not uploaded to project folder. | Go to the project folder, and click ‘Upload’ to upload your file to the folder.               |
| Step 6   | Error after running the PyCoGAPS cell | Path parameter not updated.               | Make sure to replace the default path parameter with the ‘Upload’ button to upload your data. |
