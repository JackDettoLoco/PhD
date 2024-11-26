# Microbiome Analysis Pipeline

This repository contains scripts and workflows for conducting microbiome analyses using **QIIME2** and **R**. The workflows are designed to handle metagenomic and taxonomic data, performing tasks such as sequence processing, differential abundance analysis, and visualization.

---

## Table of Contents
1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Pipeline Details](#pipeline-details)
   - [QIIME2 Workflow](#qiime2-workflow)
   - [R Workflow](#r-workflow)
4. [Usage](#usage)
5. [Outputs](#outputs)

---

## Overview

This repository supports two primary analysis pipelines:
1. **QIIME2 Workflow**: Focused on sequence processing, taxonomic classification, and phylogenetic diversity analysis.
2. **R Workflow**: Performs differential abundance analysis using ANCOMBC2 and creates detailed taxonomic visualizations.

These workflows are complementary and provide end-to-end support for microbiome data analysis.

---

## Prerequisites

### Software and Dependencies
1. **QIIME2** (v2021.8 or later)
   - Ensure all plugins like `dada2`, `feature-classifier`, `phylogeny`, and `taxa` are installed.
2. **R** (v4.0 or later)
   - Required R packages: `tidyverse`, `phyloseq`, `qiime2R`, `microbiome`, `ANCOMBC`, `microViz`, `ggplot2`, `lme4`.

### Input Files
- **QIIME2 Workflow**:
  - Raw paired-end sequences in `CasavaOneEightSingleLanePerSampleDirFmt` format.
  - A pre-trained classifier for taxonomic classification (e.g., Silva database).
  - Metadata file in `.tsv` format.
- **R Workflow**:
  - Exported `.qza` and `.qzv` files from QIIME2.
  - Metadata file with relevant grouping columns.

---

## Pipeline Details

### QIIME2 Workflow
The **QIIME2 pipeline** includes the following steps:
1. **Data Import**: Converts raw paired-end sequence data into QIIME2's `SampleData[PairedEndSequencesWithQuality]` format.
2. **Denoising with DADA2**: Removes noise and generates a feature table and representative sequences.
3. **Taxonomic Classification**: Classifies sequences using a pre-trained classifier (e.g., Silva database).
4. **Diversity Analysis**: Computes alpha and beta diversity metrics based on phylogenetic trees.
5. **Visualization**: Produces bar plots, tables, and diversity summaries.

### R Workflow
The **R pipeline** is designed for downstream statistical and visualization tasks:
1. **Import Data**: Converts exported QIIME2 `.qza` files into `phyloseq` objects.
2. **Differential Abundance Analysis**:
   - Performs ANCOMBC2 at various taxonomic levels (e.g., Phylum, Genus).
   - Identifies significant taxa with adjusted p-values and log fold changes.
3. **Visualization**:
   - Generates bar plots with error bars for log fold changes.
   - Outputs results as `.tsv` files and high-resolution images.

---

## Usage

### Running the QIIME2 Workflow
1. Update the `QIIME2` paths in the Bash script (`qiime2_workflow.sh`).
2. Execute the script:
   ```bash
   bash qiime2_workflow.sh
