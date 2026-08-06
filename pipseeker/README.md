# PIPseeker Processing

This workflow processes raw PIP-seq FASTQ files using **PIPseeker** to generate single-cell gene expression count matrices.

## Workflow overview

The workflow processes each sample independently and consists of a single analysis step.

| Step | Snakemake rule | Description | Primary outputs |
|------|----------------|-------------|-----------------|
| **1. Gene expression quantification** | `pipseeker_run` | Align sequencing reads using STAR, perform PIP-seq processing, and generate gene expression count matrices. | Gene count matrices, QC outputs, processing log |

## Prerequisites

### Input data

Required inputs include:

- Demultiplexed FASTQ files
- STAR genome index

### Software

The workflow is implemented in Snakemake and requires:

- PIPseeker
- STAR

A container can also be used (currently commented in the workflow).

## Configuration

Configure the workflow in `config.yaml`:

- `PIPSEEKER` – path to the PIPseeker executable
- `STAR_INDEX_PATH` – STAR genome index
- `CHEMISTRY_VERSION` – PIP-seq chemistry version (e.g. v4 or v5)
- `SAMPLE_ID` – list of sample IDs to process

Update any environment-specific paths before running the workflow.

## Running the pipeline

```bash
# Dry run
snakemake -np

# Run the full workflow
snakemake --profile lsf

# Run a single sample
snakemake --profile lsf processed/<sample_id>.log
```

## Outputs

For each sample, the workflow generates:

- Gene expression count matrices
- PIPseeker output files
- Quality control metrics
- Processing log (`processed/<sample_id>.log`)
