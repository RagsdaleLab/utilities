# GENETICS article template, using RMarkdown

## requirements

Manuscript compilation uses bookdown and rmarkdown. At the very least, you need:

If using conda, we can create an R environment
```sh
conda create -n r_env r-essentials r-base -y
conda activate r_env
```

We install the required R packages:
```sh
conda install --file requirements.txt
```

The required R packages are

* bookdown
* rmarkdown
* knitr
* kableExtra

## build

To build, type `make`.
