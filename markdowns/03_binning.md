### Step 2: Perform Binning

The binning step takes the rows of genomic positions and compresses them
down to 1 row for every 200 rows previously. This massively reduces the
file size and processing time in the third step.

**Do not run this command**
This step should take approximately 4 minutes to complete.

```bash
sequenza-utils seqz_binning \
-w 200 -s stage1.seqz.gz -o stage2.seqz.gz
```

Explanation of parameters:

> **-w**: the window size (typically 50 for exomes, 200 for genomes)  
> **-s**: the large seqz file generated in the first step
