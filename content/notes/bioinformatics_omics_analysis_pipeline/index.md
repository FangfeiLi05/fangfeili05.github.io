---
title: "Bioinformatics Omics Analysis Pipeline"
date: 2026-06-01
description: "Add description"
summary: "Bioinformatics"
tags: [""]
---


## Content Structure

```bash
omics-analysis-example/
│
├── data/
│   ├── raw/
│   │   ├── SRRXXXX_1.fastq
│   │   └── SRRXXXX_2.fastq
│   │
│   └── trimmed/
│       ├── clean_1.fastq
│       └── clean_2.fastq
│
├── reference/
│   ├── genome.fa
│   ├── annotation.gtf
│   └── index/
│       ├── genome_index.1.ht2
│       ├── genome_index.2.ht2
│       └── ...
│
├── results/
│   ├── alignment/
│   │   ├── aligned.sam
│   │   ├── aligned.bam
│   │   └── aligned.sorted.bam
│   │
│   ├── counts/
│   │   └── counts.txt
│   │
│   └── variants/
│
├── qc/
│   ├── raw/
│   ├── trimmed/
│   └── multiqc_report.html
│
├── logs/
│   ├── fastp.log
│   ├── hisat2.log
│   └── featurecounts.log
│
├── scripts/
│   ├── run_fastp.sh
│   ├── run_alignment.sh
│   ├── run_counts.sh
│   └── pipeline.sh
│
└── env/
    └── environment.yml
```

## Conda Environment Setup

```bash
conda env create -f env/environment.yml

conda activate omics-analysis
```

## Data Preparation

### Step 1. Download Dataset (SRA)

A small human RNA-seq dataset is used for real human RNA-seq

```bash
fasterq-dump ERR188273 --split-files -O data/raw/
```

### Step 2. Download Reference Genome (GRCh38)

```bash
wget https://ftp.ensembl.org/pub/release-111/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz

gunzip Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
mv Homo_sapiens.GRCh38.dna.primary_assembly.fa reference/genome.fa
```

### Step 3. Download Annotation (GTF)

GTF (Gene Transfer Format)

```bash
wget https://ftp.ensembl.org/pub/release-111/gtf/homo_sapiens/Homo_sapiens.GRCh38.111.gtf.gz

gunzip Homo_sapiens.GRCh38.111.gtf.gz
mv Homo_sapiens.GRCh38.111.gtf reference/annotation.gtf
```

### Step 4. Build HISAT2 Index

```bash
hisat2-build reference/genome.fa reference/index/grch38
```

## Bioinformatics Pipeline

### Step 1: Quality Control (Raw Reads)

```bash
fastqc data/raw/*.fastq -o qc/raw/
```

### Step 2. Read Trimming

```bash
fastp \
  -i data/raw/ERR188273_1.fastq \
  -I data/raw/ERR188273_2.fastq \
  -o data/trimmed/clean_1.fastq \
  -O data/trimmed/clean_2.fastq \
  -h qc/trimmed/fastp.html \
  -j qc/trimmed/fastp.json \
  -w 4
```

### Step 3: Quality Control (Trimmed Reads)


```bash
fastqc data/trimmed/*.fastq -o qc/trimmed/
```

### Step 4. Alignment (key step)

```bash
hisat2 -x reference/index/grch38 \
  -1 data/trimmed/clean_1.fastq \
  -2 data/trimmed/clean_2.fastq \
  -S results/alignment/aligned.sam
```

### Step 5. BAM Processing

```bash
samtools view -bS results/alignment/aligned.sam | samtools sort -o results/alignment/aligned.sorted.bam

samtools index results/alignment/aligned.sorted.bam

rm results/alignment/aligned.sam
```

### Step 6. Quality Control (Alignment)

```bash
samtools flagstat results/alignment/aligned.sorted.bam > logs/alignment_qc.txt
```

### Step 7. Gene Quantification (key step)

```bash
featureCounts \
  -a reference/annotation.gtf \
  -o results/counts/counts.txt \
  results/alignment/aligned.sorted.bam
```

### Step 8. Normalization (key step)

## ML Pipeline Pipeline
