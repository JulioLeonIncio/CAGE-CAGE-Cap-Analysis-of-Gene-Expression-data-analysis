# CAGE-Cap-Analysis-of-Gene-Expression-data-analysis
Repository for the analysis of CAGE data 
(By Julio Leon, 2020)
## What is CAGE?
*CAGE (Kodzius et al. 2006) is a high-throughput method for transcriptome analysis that utilizes cap trapping (Carninci et al. 1996), a technique based on the biotinylation of the 7-methylguanosine cap of Pol II transcripts, to pulldown the 5′-complete cDNAs reversely transcribed from the captured transcripts.

*CAGE provides information on two aspects of capped transcriptome: genome-wide 1bp-resolution map of TSSs and transcript expression levels

## Getting Started
This  instructions will explain how to analyze CAGE data using Perl scripts starting from fastq files or TSS bed files
## Prerequisites
Perl
Histat2

## Work-flow
1. Mapping into a genome  > Fastq to BAM
* script: 2020022113.run_hisat2_map
* Note: hisat2 and other splice-junction aware aligners can be used like STAR, tophat.
* input: fastq and hg38 hisat2 index
* output: one bam file for each sample 
2. Generate CTSS from Bam files 
* script: 
* input: bam files
* output: bed files
3. Pulling all CTSS into a big CTSS file
* script:CTSSBedPooler_v0.2.pl
* input:	a list of all ctss files
* output:	one big ctss file
  - example:
```
perl /home/julio.l/data/CAGE_CHUNG_perl_scripts/CTSSBedPooler_v0.2.pl --CTSSListPath=/home/julio.l/data/CAGE_data_senescent/ctss_path.txt --outputPrefix=JL_SC --outDir=/home/julio.l/data/CAGE_data_senescent
```

4. Convert the big ctss file into bigwig (big wiggle)  (for visualization in IGV, genome browser)
* script:CTSSToBigwig_v0.1.pl
* input: a ctss file
* output: two bigwig files (plus and minus strand bigwig files)
5. De Novo clustering using Paraclu
* script: paracluRunner_v0.2.pl
* input: pooled ctss file
* output: tssCluster bed files
6. Filtering out noise from genomic backgrounds
* script:tssClusterFilterer_v0.1.pl
* input: tssCluster bed
* output:a set of tssCluster bed files filtered at different confidence intervals
7. Annotate filtered tssClusters to genes
* Note: based on user defined upstream and downstream TSS range (--up_end5Rng= and --dn_end5Rng=), e.g. --up_end5Rng=500 and --dn_end5Rng=100 means a tssClusters will be assigned to a gene if it is within the -500 to +100bp region of the annotated TSS of a gene
* script: tssClusterAnnotator_v0.1.pl
* input: tssCluster bed $ a set of gene models (GENECODE or  FANTOMCAT)
* output: gene annotations informations per tssCluster & bed files 
8. Count the expression level of the tssClusters in each sample
* script: promoterCTSSCounter_v0.4.pl
* input: a list of ctss files & a tssCluster bed file
* output: a tssCluster based count matrix for all samples & a tssCluster based normalized expression (rle_cpm, TPM and TMM) matrix for all samples

Output files from steps 4 to 6 inspected in IGV. Regulatory element (promoter) at 5'End of the NEGR1 gene
![File inspection in IGV from 4 to 6](https://github.com/JulioLeonIncio/CAGE-CAGE-Cap-Analysis-of-Gene-Expression-data-analysis/blob/master/image.png)



## Acknowledgments
Perl scripts were developed in house by Dr. Chung from IMS RIKEN
