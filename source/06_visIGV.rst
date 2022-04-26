.. _visIGV:

========================================
Part 7: Visualize gene expression in IGV
========================================

For this part of the hands-on, you need to download some data to your computer to visualize it locally. These files are:

 * the contigs of you genome of interest ``/work/projects/embomicrobial2020/data/metaT/binning/<SAMPLE>/<MAG>.fasta.contigs.fa``
 * the .bed file you created in the last step
 * the alignment files and their indices ``/work/projects/embomicrobial2020/data/metaT/binning/<SAMPLE>/<MAG>.mt.bam``, ``/work/projects/embomicrobial2020/data/metaT/binning/<SAMPLE>/<MAG>.mg.bam``, ``/work/projects/embomicrobial2020/data/metaT/binning/<SAMPLE>/<MAG>.mt.bam.bai``, and ``/work/projects/embomicrobial2020/data/metaT/binning/<SAMPLE>/<MAG>.mg.bam.bai``
 * the filtered GFF file ``/work/projects/embomicrobial2020/data/metaT/annotations/<SAMPLE>/<MAG>.annotation_CDS_RNA_hmms.gff``

`IGV <https://software.broadinstitute.org/software/igv/download>`_ is a graphical interface for genome visualization. You can run it on your computer. Here's how you can install it: :download:`get IGV <_static/getIGV.pdf>`.

Once you have installed IGV, you can open the GUI and follow the description :download:`here <_static/runIGV.pdf>` to visualize the MAG, the metagenomics and metatranscriptomics reads that map to it, the positions of the open reading frames, and the positions of the metatranscriptomics-only contigs we were able to recover in the last step.

.. admonition:: Tasks

   Explore the variation in coverage depth in the metagenome and metatranscriptome. 

   Focus on the metatranscriptome: can you see polycistronic operons? Compare the pattern of coverage with metatransctiptomic reads to the positions of the metatranscriptome-assembled contigs. Do you see a pattern? Can you find positions with a surprising coverage depth?

   Use the search bar to find a gene with the KO annotation K00635. This is a key gene for the lipid-accumulating phenotype of *Microthrix parvicella* and the whole floating sludge community.

