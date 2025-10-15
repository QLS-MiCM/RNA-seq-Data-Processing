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

#### Alignment with STAR

--outSAMtype BAM SortedByCoordinate: this allows us to automatically generate a sorted BAM file

--limitBAMsortRAM 17179869184: We limit the ram usage to avoid crashing

--outFilterType BySJout: Filters reads based on detected splice junctions, removing reads with unconfirmed junctions.

--outFilterMultimapNmax 20: Allows reads to map to up to 20 locations; reads mapping to more are discarded.

--alignSJoverhangMin 8: Requires at least 8 bp on each side of a novel splice junction to consider it valid.

--alignSJDBoverhangMin 1: Requires at least 1 bp overhang for annotated splice junctions from the GTF.

--outFilterMismatchNmax 999: Sets a very high limit for total mismatches; effectively controlled by the relative mismatch parameter.

--outFilterMismatchNoverLmax 0.04: Allows up to 4% mismatches per read relative to read length.

--alignIntronMin 20: Sets the minimum intron length to 20 bp.

--alignIntronMax 1000000: Sets the maximum intron length to 1,000,000 bp (1 Mb).

--seedSearchStartLmax 30: Sets the maximum length of initial seed search for alignment.

#### Indexing and filtering out reads with low mapping quality scores

-F 2820: Removes reads matching any of the SAM flag bits that sum to 2820. the 2820 comprises: 4 → unmapped

    a) 8 → mate unmapped
    
    b) 256 → secondary alignment
    
    c) 512 → QC fail
    
    d) 1024 → PCR/optical duplicate
    
    e) 2048 → supplementary alignment

-q 30 (Minimum mapping quality): Keeps reads with mapping quality ≥ 30 (high-confidence alignments)

-b: Outputs BAM instead of SAM

-@ 4: Uses 4 CPU threads for faster processing
