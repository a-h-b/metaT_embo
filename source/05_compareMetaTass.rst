.. _compareAss:

============================
Part 6: metaT-only assembly?
============================

You may have only metatranscriptomic reads and wonder what you can do with them. In this part of the hands-on session, you can compare a metatranscriptomics-only assembly with the integrated metagenomics and metatranscriptomics assembly. We have picked the most dominant MAG from the dataset as an example.

Metatranscriptomics-only assemblies can be found in ``/work/projects/embomicrobial2020/data/metaT/assemblies/$mySample/final.contigs.fa``. 

Information for the example MAG is in ``/work/projects/embomicrobial2020/data/metaT/binning/$mySample/``. 

To compare the contigs from the metaT-only assembly to the MAG, you can use nucmer (make sure you request sufficient cpus (8) in your interactive slurm job):

.. code:: Console

   conda activate /work/projects/embomicrobial2020/envs/mummer4
   cpus=8
   sample=2011-07-08

   ref=final.contigs.fa
   bin=`cat /work/projects/embomicrobial2020/data/metaT/binning/$sample/bins`
   qry=$bin.contigs.fa
   prefix=$sample.genomalign

   mkdir metaTGvsmetaT
   cd metaTGvsmetaT

   nucmer -t $cpus -p $prefix /work/projects/embomicrobial2020/data/metaT/binning/$sample/$qry /work/projects/embomicrobial2020/data/metaT/assemblies/$sample/$ref

   delta=$prefix.delta
   dnadiff -p $prefix -d $delta
   show-coords $prefix.1delta >$prefix.1delta.coords

Here is a description of the output in ``$prefix.1delta.coords`` from the nucmer manual:
[S1] start of the alignment region in the reference sequence [E1] end of the alignment region in the reference sequence [S2] start of the alignment region in the query sequence [E2] end of the alignment region in the query sequence [LEN 1] length of the alignment region in the reference sequence [LEN 2] length of the alignment region in the query sequence [% IDY] percent identity of the alignment [% SIM] percent similarity of the alignment (as determined by the BLOSUM scoring matrix) [% STP] percent of stop codons in the alignment [LEN R] length of the reference sequence [LEN Q] length of the query sequence [COV R] percent alignment coverage in the reference sequence [COV Q] percent alignment coverage in the query sequence [FRM] reading frame for the reference and query sequence alignments respectively [TAGS] the reference and query FastA IDs respectively. All output coordinates and lengths are relative to the forward strand of the reference DNA sequence.

.. admonition:: Excercise

   Adapt the nucmer, dnadiff and show-coords to run the same comparison in the opposite direction (metaTGvsmetaT).

You can already see from the numbers in ``$mySample.genomalign.report`` that only a part of the MAG that was assembled from metaG and metaT reads is also assembled from the transcriptome (the 53.3175% in the example below):

.. code:: Console

   [Bases]
   TotalBases                   3252111             59671729
   AlignedBases       1733945(53.3175%)     1806914(3.0281%)
   UnalignedBases     1518166(46.6825%)   57864815(96.9719%)

.. admonition:: Excercise

   For the next step, extract the alignment information as .bed format, as shown in the code below.

.. code:: Console

   paste <(cut -f 12 /work/projects/embomicrobial2020/data/metaT/binning/$mySample/genomealignment/metaTGvsmetaT/$mySample.genomalign.1coords) <(cut -f 1,2 /work/projects/embomicrobial2020/data/metaT/binning/$mySample/genomealignment/metaTGvsmetaT/$mySample.genomalign.1coords)  >> $mySample.genomalign.bed 

Copy the resulting file to your computer.
