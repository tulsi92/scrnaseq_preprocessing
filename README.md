# cellranger_count
Snakemake pipeline to run CellRanger count step for FASTQ files from 10x Genomics scRNA-seq. Each sample will be submitted as a job to run simultaneously.

Input:
**config.yaml**
* FASTQ_DIR - path to folder where fastq files are located
* SAMPLE_ID - list sample IDs (must match name prefix in fastq files e.g. <sample1>_S1_L001_R1_001.fastq.gz)
* KEEP_BAMS - whether to keep large intermediate BAM files for other analyses (default: no)

How to run:
snakemake --profile lsf
