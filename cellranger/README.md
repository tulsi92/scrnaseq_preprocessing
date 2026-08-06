# Cell Ranger Processing

This workflow processes raw 10x Genomics scRNA-seq FASTQ files using **Cell Ranger** to generate gene expression count matrices.

## Workflow overview

The workflow processes each sample independently and consists of a single analysis step.

| Step | Snakemake rule | Description | Primary outputs |
|------|----------------|-------------|-----------------|
| **1. Gene expression quantification** | `cellranger_count` | Align sequencing reads, perform barcode and UMI correction, quantify gene expression, and generate Cell Ranger outputs. | Feature-barcode matrices, QC reports, optional BAM files |

## Prerequisites

### Input data

Required inputs include:

- Demultiplexed FASTQ files
- Cell Ranger reference transcriptome

### Software

The workflow is implemented in Snakemake and requires:

- Cell Ranger
- Snakemake

## Configuration

Configure the workflow in `config.yaml`:

- `FASTQ_DIR` – directory containing FASTQ files
- `SAMPLE_ID` – list of sample IDs
- `TRANSCRIPTOME_REF` – Cell Ranger reference transcriptome
- `KEEP_BAMS` – whether to retain BAM files (`yes` or `no`)

If `KEEP_BAMS = no`, Cell Ranger is run with the `--no-bam` option to reduce storage requirements.

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

- Filtered feature-barcode matrix
- Raw feature-barcode matrix
- Cell Ranger summary metrics
- Web summary report
- Optional BAM file
- Processing log (`processed/<sample_id>.log`)
