# pipseeker
Snakemake pipeline to run pipseeker alignment and counting step for FASTQ files from PIP-seq scRNA-seq data. Each sample will be submitted as a job to run simultaneously.

Input:

**config.yaml**
* STAR_INDEX_PATH - path to STAR aligner index file
* SAMPLE_ID - list sample IDs (must match name prefix in fastq files e.g. <sample1>_S1_L001_R1_001.fastq.gz)
* CHEMISTRY_VERSION - version of chemistry used - v4 or v5

How to run:

```snakemake --profile lsf```
