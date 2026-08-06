# scRNA-seq FASTQ Processing

This repository contains Snakemake workflows for generating gene expression count matrices from single-cell RNA-sequencing (scRNA-seq) FASTQ files.

Currently, two processing pipelines are supported:

- **Cell Ranger** for standard 10x Genomics scRNA-seq data
- **PIPseeker** for PIP-seq datasets

Each sample is processed independently, allowing jobs to be run in parallel on an HPC cluster.

## Repository structure

| Folder | Analysis | Key inputs | Key outputs |
|--------|----------|------------|-------------|
| `cellranger/` | 10x Genomics Cell Ranger pipeline | FASTQ files, Cell Ranger reference transcriptome | Filtered feature-barcode matrices, QC metrics, Cell Ranger outputs |
| `pipseeker/` | PIP-seq processing pipeline | FASTQ files, STAR reference index | Gene count matrices and PIP-seq outputs |

Each module contains:

- Detailed `README.md`
- Snakemake workflow
- Required Conda environment
- Analysis-specific configuration

## Workflow overview

The pipelines perform the following steps:

1. Read sample information from the configuration file
2. Process each sample independently
3. Align sequencing reads
4. Quantify gene expression
5. Generate count matrices and quality control outputs

## Supported analyses

| Pipeline | Description |
|----------|-------------|
| **Cell Ranger** | Alignment, barcode correction, UMI counting, and gene expression quantification for 10x Genomics scRNA-seq data. |
| **PIPseeker** | Alignment and count matrix generation for PIP-seq datasets using STAR. |

## Prerequisites

### Input data

Required inputs include:

- Demultiplexed FASTQ files
- Reference transcriptome (Cell Ranger) or STAR genome index (PIP-seq)

### Software

Depending on the workflow:

- Cell Ranger
- STAR
- Snakemake

Conda environments are provided where applicable.

## Configuration

Each workflow is configured through `config.yaml`.

Typical parameters include:

- sample IDs
- FASTQ directory
- reference transcriptome or STAR index
- chemistry version (PIP-seq)
- whether BAM files should be retained (Cell Ranger)

Update any environment-specific paths before running the workflow.

## Running the pipeline

```bash
# Dry run
snakemake -np

# Run the full workflow
snakemake --profile lsf

# Run to a specific rule
snakemake --profile lsf --until <rule_name>
```

## Outputs

Depending on the workflow, outputs include:

- Gene count matrices
- Filtered feature-barcode matrices
- Alignment files (optional)
- Cell Ranger or PIP-seq summary metrics
- Processing logs
