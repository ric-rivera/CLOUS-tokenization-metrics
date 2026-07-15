# CLOUS: Cross-Linguistic Orthographic Uniqueness Score

[![Paper](https://img.shields.io/badge/Paper-Preprint_Available-blue)](#) 
*(Link to arXiv will be added upon endorsement)*

**Official codebase for the paper:** *Estimating Cross-Lingual Tokenization Fragmentation Risk: A Frequency-Based Uniqueness Score for Geographic Entities.*

## Overview
Large language models often penalize multilingual users through hidden "tokenizer taxes" caused by subword fragmentation. Geographic proper nouns offer a controlled stress case for this distributional asymmetry, as they are standardized, cross-linguistically available entities whose orthographic forms frequently mismatch tokenizer training distributions.

This repository introduces the **Cross-Linguistic Orthographic Uniqueness Score (CLOUS)**, a character-level metric based on Shannon surprisal that quantifies the orthographic rarity of localized country names. 

Evaluated against six production tokenizers across eleven languages, CLOUS shows significant associative strength with tokenization fertility in 61 of 65 valid combinations. Furthermore, CLOUS maintains a positive correlation with fragmentation where naive length-based baselines (byte length and character count) demonstrate negative correlations, proving that CLOUS captures orthographic complexity beyond simple string length.

As a high-risk entity screening tool, CLOUS achieves ROC-AUC = 0.850 and F1 = 0.741, correctly identifying approximately three-quarters of the highest-fragmentation entities from orthographic properties alone — without model inference. CLOUS serves as a lightweight, pre-tokenization diagnostic for multilingual NLP pipelines."

## Repository Structure
The project is organized as follows:

* `Rivera_2026_CLOUS_Tokenization_V2.pdf`: The finalized manuscript and findings.
* `raw_corpora/`: Leipzig Corpora Collection character frequency files used to build language-specific profiles.
* `cache/`: Serialized JSON frequency maps, intermediate pipeline results, and the exact median statistics (`benchmark_results.csv`, `final_stats.csv`, `clous_scores.csv`).
* `CLOUS_pipeline.ipynb`: Main Google Colab notebook containing the complete reproducible evaluation pipeline.
* `results/`: Final visual outputs, including `Figure_1_CLOUS_Heatmap.png` and `Figure_2_Stratified_Scatter.png`.

## Usage
To reproduce the findings or calculate CLOUS scores for new entities:

1. Open `CLOUS_pipeline.ipynb` in Google Colab or your local Jupyter environment.
2. Ensure the `raw_corpora/` and `cache/` directories are accessible in your working directory.
3. Run the cells sequentially to compute character frequency profiles, calculate CLOUS scores, and generate the final correlation benchmarks.

## Citation
If you use CLOUS or this evaluation pipeline in your research, please cite the associated paper:

```bibtex
@article{rivera2026clous,
title={Estimating Cross-Lingual Tokenization Fragmentation Risk: A Frequency-Based Uniqueness Score for Geographic Entities},
  author={Rivera, Richard},
  year={2026},
  note={Independent Research, Preprint. arXiv preprint available at https://github.com/ric-rivera/CLOUS-tokenization-metrics}
}
