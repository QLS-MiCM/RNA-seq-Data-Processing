# QLS-MiCM RNA-seq Workshop for D2R - Day 2


This workhop covers all the processing pipeline from raw FASTQ files to count matrix for RNA-seq data

### Requirements

- A google account (to access google colab)
- Basic knoweldge of bash 

### Contents

- Link to google colab: https://colab.research.google.com/gist/almejiaga/44f8b5f888bb740c63e33d4d371ca20b/rna-seq_workshop.ipynb?authuser=1

All material for exercise can be found in the Exercise/ directory

- scripts

This is a copy of the google colab script
- data

Contains the .fastq file used to perform the analysis. The full FASTQ file can be found here: GSE250471

## Parameters used for every step of the analysis

#### Generating the STAR index for chr22

--runThreadN 6 (number of CPUs)

--sjdbOverhang 49 (it should be your read length -1): this helps STAR to generate sequences that match the length of your reads for faster alignment

--genomeSAindexNbases 11: Controls the size of the genome’s suffix array index used internally by STAR, we use 11 because it is only one chromosome
