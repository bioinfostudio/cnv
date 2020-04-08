## Sequenza Analysis Results and Visualisation

One of the first and most important estimates that Sequenza provides is
the tumour cellularity (the estimated percentage of tumour cells in the
tumour genome). This estimate is based on the B allele frequency and
depth ratio through the genome and is an important metric to know for
interpretation of Sequenza results and for other analyses. Lets look at
the cellularity estimate for our analysis by opening
`CanGenWorkshop_model_fit.pdf` with the command:

  [CanGenWorkshop_model_fit.pdf](repo:sequenza_results/CanGenWorkshop_model_fit.pdf){:target="_blank"}

The cellularity estimate is at the top along with the average ploidy
estimate and the standard deviation of the B allele frequency. We can
see that the cellularity has been estimated at 24% which is fairly low
and we will see why this is bad in the next section on CNV
visualisation. The ploidy value of 2.1 indicates this piece of the
genome is not hugely amplified or deleted and the BAF standard deviation
indicates there are no significant long losses of heterozygosity.

Let’s now look at the CNV inferences through our genomic block. Open the
genome copy number visualisation file with:

  [CanGenWorkshop_genome_view.pdf](repo:sequenza_results/CanGenWorkshop_genome_view.pdf){:target="_blank"}

This file contains three "pages" of copy number events through the
entire genomic block.

1. The first page shows copy numbers of the A (red) and B (blue) alleles,
2. The second page shows overall copy number changes, and
3. The third page shows the B allele frequency and depth ratio through
genomic block.  

Looking at the overall copy number changes, we see that
our block is at a copy number of 2 with a small duplication to copy
number 4 about 1/3 of the way through the block and another just after
halfway through the block. There is also a reduction in copy number to 1
copy about 4/5 of the way through the block. The gap that you see just
before this reduction in copy number is the chromosomal centromere - an
area that is notoriously difficult to sequence so always ends up in a
gap with short read data.

You can see how this is a very easy to read output and lets you
immediately see the frequency and severity of copy number events through
your genome. Let’s compare the small genomic block we ran with the same
output from the entire genome which has been pre-computed for you. This
is located in the `pre_generated/results_whole_genome` folder and
contains the same 13 output files as for the small genomic block. As
before, let’s look at the cellularity estimate with:

  [CanGenWorkshop_model_fit.pdf](repo:pre_generated/results_whole_genome/CanGenWorkshop_model_fit.pdf){:target="_blank"}

It now looks like it’s even worse at just 16%! A change is to be
expected as we were only analysing 1.9% of the genome. Let’s now look at
the whole genome copy number profile with:

  [CanGenWorkshop_genome_view.pdf](repo:pre_generated/results_whole_genome/CanGenWorkshop_genome_view.pdf){:target="_blank"}

You can see that there are a number of copy number events across the
genome and our genomic block (the first 60Mb of chromosome 5) is
inferred as mostly copy number 4 followed by a reduction to copy number
2, rather than 2 to 1 as we saw in the output we generated. The reason
for this is that `Sequenza` uses the genome-wide depth ratio and BAF in
order to estimate copy number, if you ask it to analyse a small block
mostly at copy number 4 with a small reduction to copy number 2, the
most likely scenario in lieu of more data is that this is a copy number
2 block with a reduction to 1. It’s important to carefully examine the
cellularity, ploidy and BAF estimates of your sample along with the
plots of model fit (`CanGenWorkshop_model_fit.pdf`) and
cellularity/ploidy contours (`CanGenWorkshop_CP_contours.pdf`) in order
to decide if you believe Sequenza’s inference of the copy numbers. Have
a look at these for yourself if you want to get a better idea of how
`Sequenza` makes its inferences and conclusions.
