# GenomeAnalysis
The Genome Analysis Pipeline enables accurate variant detection and evaluation using powerful bioinformatics tools like GATK, Samtools, FastQC, with reference genomes hg19 or GRCh38.
# 1. Data Preprocessing
Data preprocessing is a crucial step to ensure high-quality input data before variant analysis.

- Quality Control (QC): Use FastQC to assess the quality of sequencing reads.
- Trimming & Filtering: Remove low-quality bases and adapter sequences using tools like Trimmomatic or Cutadapt.
- Alignment (Mapping): Align reads to the reference genome (hg19 or GRCh38) using BWA-MEM or Bowtie2, generating BAM/SAM files.
- Sorting & Indexing: Sort and index BAM files using Samtools or Picard.
- Mark Duplicates: Remove duplicate reads with Picard MarkDuplicates to reduce bias.
- Base Quality Score Recalibration (BQSR): Adjust base quality scores using GATK BaseRecalibrator to minimize sequencing errors.
# 2. Germline Short Variant Discovery (GATK)
The goal is to identify SNPs (Single Nucleotide Polymorphisms) and Indels (Insertions & Deletions) from human genome data.

- HaplotypeCaller: Use GATK HaplotypeCaller for variant calling.
- CombineGVCFs: Merge multiple GVCF files from different samples into a single file.
- GenotypeGVCFs: Convert GVCF into VCF containing identified variants.
- Variant Filtration: Apply quality filters such as DP (Depth), QD (Quality by Depth), MQ (Mapping Quality) using GATK VariantFiltration.
# 3. Callset Refinement
After variant calling, refinement is needed to improve accuracy.

- Variant Recalibration (VQSR): Use GATK VariantRecalibrator to refine variant quality using a machine learning model.
- Hard Filtering: If no training data is available, apply hard filtering criteria (e.g., QD < 2.0, FS > 60.0, MQ < 40).
- Normalize Variants: Use vt normalize to standardize variant representation.
# 4. Callset Evaluation
Evaluating the variant callset ensures data quality and pipeline correctness.

- Concordance Analysis: Compare against gold-standard variant datasets like dbSNP, 1000 Genomes, gnomAD.
- Functional Impact Analysis: Assess variant effects using SnpEff or ANNOVAR.
- Variant Density Plots: Check the distribution of variants across the genome using bcftools stats and plot-vcfstats.
# 5. Annotate Variants
Variant annotation provides biological and clinical insights.

- VEP (Variant Effect Predictor): Predicts the impact of variants on genes and proteins.
- dbSNP & ClinVar Annotation: Cross-reference with clinical databases to identify disease-related variants.
- Pathogenicity Prediction: Use PolyPhen and SIFT to assess variant pathogenicity.
# 6. Somatic Short Variant Discovery
Identifying somatic variants, especially in cancer data, by comparing tumor vs normal samples.

- Mutect2 (GATK): Detect somatic variants from paired tumor-normal data.
- FilterMutectCalls: Remove false positives to improve variant accuracy.
- MSI & TMB Analysis: Analyze Microsatellite Instability (MSI) and Tumor Mutational Burden (TMB) to characterize tumor profiles.
