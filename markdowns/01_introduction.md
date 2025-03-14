## Introduction

The goal of this hands-on session is to perform a copy number variation
analysis (CNV) on a normal/tumour pair of alignment files (BAMs)
produced by the mapping of Illumina short read sequencing data.

To ensure reasonable analysis times, we will perform the analysis on a
heavily subsetted pair of BAM files. These files contain just the first
60Mb of chromosome 5 but contain several examples of inferred copy
number events to enable interpretation and visualisation of the copy
number variation that is present in entire cancer genomes. `Sequenza` is
the tool we will use to perform this analysis. It consists of two
`Python` pre-processing steps followed by a third step in `R` to infer the
depth ratio, cellularity, ploidy and to plot the results for
interpretation.

In the second part of the tutorial we will also be using `IGV` to
visualise and manually inspect the copy number variation we inferred in
the first part for validation purposes. This section will also include a
discussion on the importance of good quality data by highlighting the
inadequacies of the workshop dataset and the implications this has on
analysis results.

## Prepare the Environment

We will use a dataset derived from whole genome sequencing of a
33-yr-old lung adenocarcinoma patient, who is a never-smoker and has no
familial cancer history.

The data files are contained in the subdirectory called `data` and are
the following:

>  `normal.chr5.60Mb.bam` and `normal.chr5.60Mb.bam.bai`

>  `tumour.chr5.60Mb.bam` and `tumour.chr5.60Mb.bam.bai`

These files are based on subsetting the whole genomes derived from `blood`
and `liver metastases` to the first 60Mb of chromosome 5. This will allow
our analyses to run in a sufficient time during the workshop, but it’s
worth being aware that we are analysing just 1.9% of the genome which
will highlight the length of time and resources required to perform
cancer genomics on full genomes!

Open the Terminal and go to the `cnv` working directory:

```bash
cd /home/bioinfo/cnv/
```

All commands entered into the terminal for this tutorial should be from
within the **`cnv`** directory.


Check that the `data` directory contains the above-mentioned files by
typing:

```bash
ls -l data
```
