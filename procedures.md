---

hero_image: /jubilant-bassoon/images/hero.jpg
<!-- hero_height: is-fullwidth -->
hero_darken: true

---

## Installing CoGAPS

CoGAPS is a bioconductor package and so the release version can be installed as follows:
```yaml
source("https://bioconductor.org/biocLite.R")
biocLite("CoGAPS")
```
The most up-to-date version of CoGAPS can be installed directly from the <a href="https://github.com/FertigLab/CoGAPS" target="_blank">FertigLab Github Repository</a>:
```yaml
## Method 1 using biocLite
biocLite("FertigLab/CoGAPS", dependencies = TRUE, build_vignettes = TRUE)

## Method 2 using devtools package
devtools::install_github("FertigLab/CoGAPS")
```
There is also an option to install the development version of CoGAPS, while this version has the latest experimental features, it is not guaranteed to be stable.
```yaml
## Method 1 using biocLite
biocLite("FertigLab/CoGAPS", ref="develop", dependencies = TRUE, build_vignettes = TRUE)

## Method 2 using devtools package
devtools::install_github("FertigLab/CoGAPS", ref="develop")
```
