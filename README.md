# AtacSeq_Analysis
Atac-Seq was performed on MCF7, with two biological replicates to assess the role of cohesin in the epigenetic regulation of the 6q25.1 locus. Knockdown of the Rad21 subunit of the cohesin complex was achieved through siRNA. A non-targeting siRNA was used as a control. The library was sequenced as paired-end reads with Illumina HiSeq by New Zealand Genomics Limited (NZGL). Demultiplexing was also performed by NZGL.

# Software
FastQC v0.11.8, multiqc 1.13.dev0, cutadapt 1.18, bowtie2 2.5.0, samtools 1.15.1, sed 4.2.2, picard 2.27.4, Genrich 0.6.1, bedtools v2.30.0

# Quality Control
FastQC was used to assess read quality and MultiQC was used to compare quality metrics between samples before and after read processing.   

# Adapter Trimming
Sequencing adapters were trimmed using cutadapt in paired-end mode, requiring a minimum overlap of 13 bases between the adapter sequence and read to be trimmed. Untrimmed reads, or reads less than 20bp were discarded.  

# Mapping
Trimmed PE reads were mapped to the hg19 genome using bowtie2 in --very-sensitive mode to prioritise alignment accuracy. 

# Filtering
Mitochondrial reads and reads mapping to random contigs were removed from sam files using sed. Mapped reads were then converted into bam files using samtools and were filtered to remove unmapped reads or reads with a Q score of less than 30. Only properly aligned PE reads were retained. Duplicate reads were removed using picard MarkDuplicates function.  

# Check Insert Size
Fragment size distribution was performed on sorted bam files using the Picard CollectInsertSizeMetrics function to assess the quality of the Atac-Seq experiment. 

# Peak Calling
Peaks were called in with Genrich in multi-mapping Atac-Seq mode.

# Differential Analysis 
Differential analysis was undertaken in R Studio using the DiffBind package.

# Generation of BigWig files 
To generate BigWig files sorted bam files were converted into shifted bed files to account for the insertion of the Tn5 transposase using bedtools and a custom awk script. The resulting bed files were convert to bedgraph using bedtools genomeCoverageBed and scaled to RPGC. Subsequent bedgraphs files were then converted to bigwig files using the UCSC Genome Browser tool bedGraphToBigWig.




