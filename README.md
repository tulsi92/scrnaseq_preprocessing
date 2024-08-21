# Processing of scRNAseq FASTQ - alignment and counting
Snakemake pipeline to process FASTQ files from 10x Genomics using CellRanger or PIP-seq data using pipseeker. Each sample will be submitted as a single job to run simultaneously.

Cellranger Input:
**config.yaml**
* FASTQ_DIR - path to folder where fastq files are located
* SAMPLE_ID - list sample IDs (must match name prefix in fastq files e.g. <sample1>_S1_L001_R1_001.fastq.gz)
* KEEP_BAMS - whether to keep large intermediate BAM files for other analyses (default: no)

https://www.10xgenomics.com/support/software/cell-ranger/latest/analysis/running-pipelines/cr-gex-count

Pipseeker Input:
**config.yaml**
* STAR_INDEX_PATH - path to STAR aligner index file
* SAMPLE_ID - list sample IDs (must match name prefix in fastq files e.g. <sample1>_S1_L001_R1_001.fastq.gz)
* CHEMISTRY_VERSION - chemistry version v4 or v5

How to run in respective folders:

```snakemake --profile lsf```

Pending:
* Merge pipelines into one and add input functions to decide which tool to run
