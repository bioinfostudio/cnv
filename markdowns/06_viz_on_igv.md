## CNV Visualisation/Confirmation in IGV

Let’s see if we can visualise one of the CNV events where copy number
increased significantly. We’ll focus on the copy number 4 event seen at
about 1/3 of the way through the `CanGenWorkshop_genome_view.pdf` output
we generated. First, we need to find the coordinates that have been
predicted for this event. Have a look at the `CanGenWorkshop_segments.txt`
file in the results folder to view all predicted CNV events with:

  ```
  less sequenza_results/CanGenWorkshop_segments.txt
  ```

There is only one at a copy number of 4 (CNt column) and it starts at
21,051,700 to 21,522,065 which is 470kb and corresponds to the small block
we see in the genome view PDF.

Quit out of viewing the segments file by pressing `q`.

We will now open `IGV` and see if we can observe the predicted increase in
copy number within these genomic coordinates.

For a duplication of this size, we will not be able to easily observe it
just by looking at the raw read alignments. In order to see it we will
generate two tiled data files (TDFs) within IGV which contain the
average read depth for a given window size through the genome. This
means that we can aggregate the average read depth over relatively large
chunks of the genome and compare these values between the normal and
tumour genomes.

To begin, we will go to `Tools` then `Run igvtools...` in the IGV
menubar. Specify the normal bam file (under `cnv` then `data`) as the
input file and change the window size to 100,000 (one hundred thousand).
Then press the `Run` button and IGV will make the TDF file. This takes
about 5 minutes. **Repeat this for the tumour genome.**

After you have both TDF files, go to `File` and `Load from file...` in
the menubar and select the BAM and TDF files to open. Once you have
opened them, they will appear as tracks along with the BAM tracks we
loaded initially. Navigate to the genomic coordinates of our event
(5:21,051,700-21,522,065) by typing it in the coordinate box at the top.
Mouse over the two blue tracks to get the average depth values for the
100,000 bp windows. What you should see is that the liverMets sample has
3-6X more coverage than the Blood sample for the four windows that cover
this region.

This may seem a bit underwhelming, after all, wasn’t the increase of the
region to a copy number of 4, i.e. we expect a doubling of reads in the
tumour? To explain why we are only seeing such a small coverage
increase, we need to turn to our good friend mathematics!

Imagine we have two 30X genomes for the normal and tumour samples and
the tumour is at 100% purity. If there is a copy number increase to 4 in
the tumour from 2 in the normal, the duplicated segment should indeed
have twice as many reads as the same segment in the normal genome. Now,
lets imagine the tumour genome was only at a purity of 50% (i.e. it
contains 50% normal cells and 50% tumour cells). Now, half of the
duplicated "tumour genome" segment will be at a copy number of 2 and
half will be at 4. What does this mean when we sequence them as a
mixture? The resulting average copy number of the block will be
\((0.5*2)+(0.5*4) = 3\). Now what if we only have 16% tumour cells in our
"tumour genome"? This will be \((0.84*2)+(0.16*4) = 2.32\). You can see
how sequencing a low cellularity tumour at a low depth makes it much
harder to infer copy number variations!

Returning to our genomes at hand, when we previously looked at the
cellularity estimate of this tumour we saw it was 20% from the small
block we ran or 16% from the whole genome. Thus, the read depth increase
of just 3-6X (about 10-20% more reads) in this segment is not
surprising. A low cellularity tumour greatly reduces our power to infer
copy number events as relatively small changes in depth can occur by
chance in the genome and these can be mis-identified as copy number
changes. As well as this, it reduces our power for other analyses since
we must also remember that a tumour can itself contain multiple clones
which have to share just 16% of reads.

It is possible to sequence through a low-cellularity sample when, for
example, there is no way to take another sample (as is the case of most
biopsies). "Sequencing through" means to simply sequence the tumour at a
much higher coverage, usually 90-120X. This will mean that there will be
a net increase in reads supplying evidence for copy number events and
variants and in aggregate these will still retain power to infer these
events when using tools that look at the whole genome like Sequenza
does.
