# Relative Contributions of Donor, Recipient, and Compatibility Factors in Predicting Faecal Microbiota Transplantation Outcomes

This repository contains the code and processed data used in my undergraduate dissertation at Imperial College London investigating the relative importance of donor microbiome characteristics, recipient microbiome characteristics, and donor–recipient compatibility in predicting faecal microbiota transplantation (FMT) outcomes.

## Project Overview

Faecal microbiota transplantation (FMT) is an effective treatment for recurrent *Clostridioides difficile* infection (CDI) and has shown promise for inflammatory bowel disease (IBD). However, the factors determining treatment success remain unclear.

Using publicly available 16S rRNA gene sequencing datasets, this project aimed to compare the predictive power of:

- Donor-derived microbiome features
- Recipient-derived microbiome features
- Donor–recipient compatibility features

Random Forest machine learning models were used to evaluate the contribution of each feature category to FMT outcome prediction.

<p align="center">

  <img src="Data collection-2.png" width="800">

</p>

## Main Findings

- Donors associated with unsuccessful FMT outcomes exhibited significantly greater Shannon diversity and genus richness.
- Successful donor–recipient pairs displayed significantly greater Bray–Curtis dissimilarity prior to transplantation.
- Recipient-derived microbiome features provided the strongest predictive signal for FMT outcome.
- The recipient-only Random Forest model achieved the highest predictive performance (ROC-AUC = 0.626).
- Feature ablation analysis identified recipient-derived features as the primary drivers of model performance.
- These findings support a shift away from donor-centric explanations of FMT efficacy towards a greater emphasis on recipient ecology and donor–recipient microbial interactions.

---

## Repository Structure

```text
data_processing/
    QIIME 2 and preprocessing scripts used for 16S rRNA sequence processing

data/
    Processed genus-level relative abundance tables and metadata

diversity_analysis/
    Alpha diversity, beta diversity, PCoA, PERMANOVA, and statistical analyses

machine_learning/
    Feature matrix construction and Random Forest model training

feature_ablation/
    Combined model and feature ablation analyses

figures/
    Scripts used to generate dissertation figures

results/
    Model outputs, feature importance results, and summary tables
```

---

## Workflow

### 1. 16S rRNA Gene Sequence Processing

Raw FASTQ files were processed using QIIME 2 (v2019.10) and DADA2:

```text
FASTQ files
    ↓
Quality control and denoising
    ↓
Taxonomic assignment (SILVA 132)
    ↓
Genus-level abundance tables
    ↓
Relative abundance normalisation
```

### 2. Diversity Analyses

The processed genus-level abundance tables were used to calculate:

- Shannon diversity
- Genus richness
- Pielou's evenness
- Bray–Curtis dissimilarity

Community composition was visualised using Principal Coordinates Analysis (PCoA) and tested using PERMANOVA.

### 3. Machine Learning

Three feature matrices were constructed.

#### Donor-only model

Features:

- Top 20 most prevalent donor genera
- Donor Shannon diversity
- Donor richness
- Donor evenness

#### Recipient-only model

Features:

- Top 20 most prevalent recipient genera
- Recipient Shannon diversity
- Recipient richness
- Recipient evenness

#### Compatibility-only model

Features:

- Bray–Curtis dissimilarity
- Δ Shannon diversity
- Δ Richness
- Δ Evenness

Random Forest models were trained using repeated 10-fold cross-validation (5 repeats) and evaluated using ROC-AUC.

### 4. Combined Model and Feature Ablation

A combined Random Forest model incorporating all feature categories was constructed.

Feature group ablation was then performed by systematically removing:

- Donor-derived features
- Recipient-derived features
- Compatibility-derived features

The contribution of each feature category was quantified as the change in ROC-AUC relative to the full model.

---

## Software and Packages

### Bioinformatics

- QIIME 2 (2019.10)
- DADA2
- SILVA 132 database

### R Packages

- tidyverse
- vegan
- caret
- ranger
- pROC
- ggplot2
- readxl
- openxlsx

---

