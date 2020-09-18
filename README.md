# CAGE-Cap-Analysis-of-Gene-Expression-data-analysis
Repository for the analysis of CAGE data 
(By Julio Leon, 2020)
## What is CAGE?
*CAGE (Kodzius et al. 2006) is a high-throughput method for transcriptome analysis that utilizes cap trapping (Carninci et al. 1996), a technique based on the biotinylation of the 7-methylguanosine cap of Pol II transcripts, to pulldown the 5′-complete cDNAs reversely transcribed from the captured transcripts.

*CAGE provides information on two aspects of capped transcriptome: genome-wide 1bp-resolution map of TSSs and transcript expression levels

## Getting Started
This instructions will explain how to analyze CAGE data using Perl scripts starting from fastq files or TSS bed files
## Prerequisites
Perl
Histat2

## Work-flow
1. Mapping into a genome  > Fastq to BAM
2. Generate CTSS from Bam files 
3. Pulling all CTSS into a big CTSS file
4. Convert the big ctss file into bigwig (big wiggle)  (for visualization in IGV (genome browser))
5. De Novo clustering using Paraclu
6. Filtering out noise from genomic backgrounds
7. Annotate filtered tssClusters to genes
8. Count the expression level of the tssClusters in each sample

Output files from steps 4 to 6 inspected in IGV. Regulatyor element (promoter) at 5'of the NEGR1 gene
![File inspection in IGV from 4 to 6](https://github.com/JulioLeonIncio/CAGE-CAGE-Cap-Analysis-of-Gene-Expression-data-analysis/blob/master/image.png)



## Acknowledgments
Perl scripts were developed in house by Dr. Chung from IMS RIKEN
