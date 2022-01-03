
# (*forked*) SCISSOR [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.4269205.svg)](https://doi.org/10.5281/zenodo.4269205) 

## 🍴 Leda's forked version: modified version of SCISSOR's `build_gaf` function

SCISSOR's `build_gaf` function seems to have been modified, and the `Gene` argument seems to have been removed. `build_gaf` also browses through the whole GTF file (input) and exports the regions (the exons per gene, in a concatenated string form) for all genes included in the annotation file. This significantly increases runtime, whereas no option to select for genes of interest is given.

R code for modified function: [BuildExonsFromGTF_GeneSelection.R](https://github.com/LedaKatopodi/SCISSOR/blob/master/R/BuildExonsFromGTF_GeneSelection.R)

In this modified version:

1. A list with genes of interest can be supplied as argument. The function subsets the input file, and returns only the regions (exons) for the selected genes. If no gene list is specified, the function operates on the initial input file and will return the regions for all genes present in the annotation.

2. The function prioritizes a single annotation source for which to return the regions. Annotation priority is as follows: **Ensembl-Havana > Ensembl > Havana**. This was done in hope of alleviating issues similar to those described in [issue hyochoi#3](hyochoi#3), which seem to stem from the concatenation of exons from all available sources. The annotation prioritization was based on the fact that *"for human and mouse, this combined Ensembl/HAVANA gene set is the default gene set from the GENCODE project"* ([source](https://useast.ensembl.org/info/genome/genebuild/annotation_merge.html)).

**DISCLAIMER**: The provided code was tested only for a small number of genes (6) on mouse (Mus musculus, GRCm38, Ensembl 98); R version = 4.0.1. Possible discrepancies for different GTF files.

If you find any bugs, feel free to open a ticket.

---

## Shape Changes In Selecting Sample Outliers in RNA-seq

## Overview

`SCISSOR` (shape changes in selecting sample outliers in RNA-seq) aims for unsupervised screening of a range of structural alterations in RNA-seq data. `SCISSOR` considers a novel shape property of aligned short read data through a base-level pileup file. This intact and uncompressed view of RNA-seq profile enables the unbiased discovery of structural alterations by looking for anomalous shapes in expression. This approach holds promise for identifying otherwise obscured genetic aberrations. As a result, `SCISSOR` identifies known as well as novel aberrations including abnormal splicing, intra-/intergenic deletions, small indels, alternative transcription start/termination. 

## Documentation

The documentation is available at [https://hyochoi.github.io/SCISSOR](https://hyochoi.github.io/SCISSOR)

## System Requirements

This package has been tested on the following systems:

* macOS: Mojave (10.14.6)  
* Linux: CentOS (7.5)

## R package dependencies

`SCISSOR` requires the following packages:

* `BiocManager`
* `Rsamtools`   
* `GenomicRanges`  
* `refGenome`   
* `RColorBrewer`   
* `wesanderson`   
* `nloptr`  
* `zoo`


## Installation Guide

1. install `devtools`:

```r
if ("devtools" %in% rownames(installed.packages()) == FALSE) {install.packages("devtools")}
library(devtools)
```

2. install `SCISSOR`:

```r
install_github("hyochoi/SCISSOR")
library(SCISSOR)
```

Installation takes 5-10 mins. 

**Note:**  

If you see errors like the following: 
```r
‘rlang’ 0.3.4 is already loaded, but >= 0.4.0 is required
```
try this:
```r
devtools::install_github("r-lib/rlang", build_vignettes = TRUE)
```




