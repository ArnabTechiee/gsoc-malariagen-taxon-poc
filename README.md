# MalariaGEN GSoC '26 PoC: Alignment-Free ML Taxon Classifier 🧬🤖

**Author:** Arnab Mondal  
**Target Organization:** MalariaGEN (`malariagen-data-python`)  
**Project:** Building a machine-learning taxon classifier for genomic classification in malaria mosquitoes

## 📌 Overview
This repository contains a Proof of Concept (PoC) Jupyter Notebook demonstrating a lightweight, alignment-free approach to classifying *Anopheles* mosquito species directly from raw FASTQ reads. 

The goal of this PoC is to prove that we can bypass computationally expensive genomic alignment tools (like BWA/GATK) by treating DNA sequences mathematically, allowing for rapid taxon routing on standard hardware.

## 🔬 Methodology
1. **Biological Simulation:** Generates an ancestral 50,000bp sequence and simulates evolutionary divergence (mutation) to create three sibling species profiles (*An. gambiae, An. coluzzii, An. arabiensis*).
2. **Sequencing Simulation:** Extracts 150bp reads to mimic standard Illumina outputs, injecting a 1% machine error rate to ensure model robustness against real-world noise.
3. **Feature Extraction (Alignment-Free):** Uses a `TfidfVectorizer` to extract weighted 5-mer frequencies. This down-weights common sequences shared across all mosquitoes and amplifies the unique "words" that define a specific taxon.
4. **Classification:** Feeds the sparse k-mer matrices into a `RandomForestClassifier`.

## 📊 Results
The model successfully classifies unaligned, noisy 150bp reads with **93% accuracy**. 

Crucially, the Confusion Matrix demonstrates biological validity: it perfectly isolates *An. arabiensis*, while showing minor, expected confusion between the notoriously close sibling species *An. gambiae* and *An. coluzzii*. 

## 🚀 Next Steps (175-Hour Proposal)
The full GSoC project will focus on scaling this k-mer/ML methodology to handle massive, real-world FASTQ datasets utilizing `Xarray` and `Zarr` for high-performance, multidimensional array computing within the `malariagen_data` ecosystem.
