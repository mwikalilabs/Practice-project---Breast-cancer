# Practice-project---Breast-cancer
## RNA-seq practice: TNBC tumour sample (SRR1027172)

Practice project to learn the RNA-seq workflow using a public sample.

**Project:** RNA-seq analysis of a triple-negative breast cancer sample

**Research question:** Which genes are expressed in this breast cancer sample, and what do they suggest about its biology?

## Data
- Study: GSE52194 / SRP032789 (breast cancer subtypes and normal organoids)
- Sample: SRR1027172, triple-negative breast cancer tumour, paired-end
- Found via NCBI SRA: https://www.ncbi.nlm.nih.gov/sra/SRR1027172

## Workflow
1. Download: "prefetch SRR1027172"
2. Convert to FASTQ: "fasterq-dump --split-files SRR1027172"
3. Check stats: "seqkit stats *.fastq"
4. QC: "fastqc *.fastq"
5. Trimming: Trimmomatic (paired outputs kept)
6. QC after trimming: FastQC
7. Subset: first 1 million read pairs (`head -n 4000000`), not the full 16 million
8. Reference: chromosome 21 + GTF
9. Index: "hisat2-build ..."
10. Align: HISAT2, then "samtools sort"
11. Count: "featureCounts ..."
12. Analysis in pandas: see notebook "Breast_cancer_practice_project.ipynb"
13. Gene annotation: Ensembl BioMart (`breastcancer_mart_export.txt`)

## Results
- Alignment summary: see "align_summary.txt"
- Of the 900 chr21 genes, 244 had at least one read
- Top expressed genes: COL6A1, COL6A2 (stromal), MX1 (interferon response), APP, CSTB, HMGN1, TTC3 and PTTG1IP
- Four top hits were pseudogenes of housekeeping genes, an artefact of aligning to chr21 only
- These observations come from one sample, so they don't show that the genes are higher than in normal breast tissue

## Limitations
Only one sample was used, aligned to only one chromosome. There was no comparison group, so no differential expression.

## Tools practiced
SRA Toolkit, FastQC, Trimmomatic, HISAT2, samtools, Subread, Ensembl, Python (pandas, seaborn)
