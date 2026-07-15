# CLOUS: Cross-Linguistic Orthographic Uniqueness Score

Official codebase for the paper: Estimating Cross-Lingual Tokenization Fragmentation Risk: A Frequency-Based Uniqueness Score for Geographic Entities.

## Overview
Subword tokenizers distribute vocabulary coverage unevenly across languages and scripts, concentrating entries on character sequences that are frequent in training corpora. Geographic proper nouns are a reproducible stress case for this distributional asymmetry.

This repository introduces the Cross-Linguistic Orthographic Uniqueness Score (CLOUS), a character-level metric based on Shannon surprisal that quantifies the orthographic rarity of localized country names. Evaluated against six production tokenizers across eleven languages, CLOUS shows significant associative strength with tokenization fertility, outperforming naive length-based baselines. CLOUS serves as a lightweight pre-tokenization diagnostic for multilingual NLP pipelines.

## Repository Structure
The project is organized as follows:
* `raw_corpora/`: Leipzig Corpora Collection character frequency files used to build language-specific profiles.
* `cache/`: Serialized JSON frequency maps and intermediate pipeline results (benchmark_results.csv, final_stats.csv, and clous_scores.csv).
* `CLOUS_pipeline.ipynb`: Main Google Colab notebook containing the complete reproducible evaluation pipeline.
* `results/`: Final outputs, including Figure_1_CLOUS_Heatmap.png, Figure_2_Stratified_Scatter.png

## Usage
To reproduce the findings or calculate CLOUS scores for new entities:
1. Open `CLOUS_pipeline.ipynb` in Google Colab or your local Jupyter environment.
2. Ensure the `raw_corpora/` and `cache/` directories are accessible in your working directory.
3. Run the cells sequentially to compute character frequency profiles, calculate CLOUS scores, and generate the final correlation benchmarks.

## Citation
If you use CLOUS in your research, please cite the associated paper:

```bibtex
@article{rivera2026clous,
  title={Estimating Cross-Lingual Tokenization Fragmentation Risk: A Frequency-Based Uniqueness Score for Geographic Entities},
  author={Rivera, Richard},
  year={2026},
  note={Independent Research}
}