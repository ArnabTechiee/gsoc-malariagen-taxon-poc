# MalariaGEN GSoC 2026: Alignment-Free Machine Learning Taxon Classifier

**Author:** Arnab Mondal  
**Target Organization:** MalariaGEN (`malariagen-data-python`)  
**Project:** Building a machine-learning taxon classifier for genomic classification in malaria mosquitoes

## Abstract
This repository contains a Proof of Concept (PoC) demonstrating a lightweight, alignment-free approach to classifying *Anopheles* mosquito species directly from raw FASTQ sequence reads. 

The primary objective of this PoC is to evaluate the feasibility of bypassing computationally expensive genomic alignment pipelines (e.g., BWA, GATK) by leveraging natural language processing (NLP) techniques and ensemble machine learning. This approach aims to provide a rapid, computationally inexpensive utility for routing samples to appropriate downstream genomic resources.

## Methodology

### 1. Data Simulation
To establish a biologically realistic baseline without requiring massive raw datasets, the pipeline simulates:
* **Evolutionary Divergence:** Generation of an ancestral 50,000 bp sequence, followed by simulated mutation rates to create three distinct species profiles (*An. gambiae*, *An. coluzzii*, and *An. arabiensis*).
* **Sequencing Noise:** Extraction of 150 bp reads (mimicking standard Illumina outputs) with an injected 1% base substitution error rate to ensure the model remains robust against real-world sequencing artifacts.

### 2. Feature Engineering
The pipeline utilizes an alignment-free feature extraction method:
* **TF-IDF k-mer Extraction:** Raw sequence strings are processed using a Term Frequency-Inverse Document Frequency (`TfidfVectorizer`) algorithm operating on 5-mers. This mathematical transformation down-weights ubiquitous k-mers shared across the *Anopheles* genus while isolating and amplifying the unique sequence signatures that define specific taxa.

### 3. Model Architecture
* The resulting sparse matrices are passed into a `RandomForestClassifier`. This ensemble method was selected for its high performance on high-dimensional, sparse datasets and its ability to run efficiently on standard CPU hardware.

## Results
The baseline model successfully classifies unaligned, noisy 150 bp reads with a **93% accuracy rate**. 

Furthermore, the resulting Confusion Matrix demonstrates strong biological validity. The model effectively isolates *An. arabiensis* with near-perfect precision, while exhibiting minor, expected statistical overlap between the notoriously close sibling species *An. gambiae* and *An. coluzzii*.

## Future Scope: GSoC 2026 Proposal
The complete 175-hour GSoC project will focus on transitioning this foundational k-mer/ML methodology into production. Key objectives will include:
* Scaling the feature extraction pipeline to handle massive, real-world FASTQ datasets.
* Integrating the model directly into the `malariagen_data` ecosystem utilizing `Xarray` and `Zarr` for high-performance, multidimensional array computing.
* Packaging the classifier as an accessible, standalone API endpoint for researchers.

## Dependencies
* `numpy`
* `pandas`
* `scikit-learn`
* `matplotlib`
* `seaborn`
