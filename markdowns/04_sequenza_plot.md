### Step 3: Running Sequenza Algorithms and Plotting Results

We will now perform the CNV analysis and output the results using the `R`
part of Sequenza.

Open the `R` terminal:

```bash
R
```

You should now see the `R` prompt identified with ">".

Run the Sequenza `R` commands:

```R
library("sequenza")
setwd("/home/bioinfo/cnv")
data.file <- "stage2.seqz.gz"
seqzdata <- sequenza.extract(data.file)
CP.example <- sequenza.fit(seqzdata)
sequenza.results(sequenza.extract = seqzdata, cp.table = CP.example, sample.id = "CanGenWorkshop", out.dir="sequenza_results")
```

Quit `R`:  

```R
q()
```  

Then enter `n` at the "Save workspace image" prompt.

If every command ran successfully, you will now have a `sequenza_results`
folder containing 13 files (type `ls -l sequenza_results/`).
