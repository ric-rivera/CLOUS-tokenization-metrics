# CLOUS: Cross-Linguistic Orthographic Uniqueness Score

Official codebase for the paper: **Predicting Cross-Lingual Tokenization Fragmentation: A Frequency-Based Uniqueness Score for Geographic Entities**[cite: 1].

## Overview
Subword tokenizers distribute vocabulary coverage unevenly across languages and scripts, concentrating entries on character sequences that are frequent in training corpora[cite: 1]. Geographic proper nouns are a reproducible stress case for this distributional asymmetry[cite: 1]. 

This repository introduces the Cross-Linguistic Orthographic Uniqueness Score (CLOUS), a character-level metric based on Shannon surprisal that quantifies the orthographic rarity of localized country names[cite: 1]. Evaluated against six production tokenizers across eleven languages, CLOUS shows significant associative strength with tokenization fertility, outperforming naive length-based baselines[cite: 1]. CLOUS serves as a lightweight pre-tokenization diagnostic for multilingual NLP pipelines[cite: 1].

## Repository Structure
The project is organized as follows:
* **`raw_corpora/`**: Leipzig Corpora Collection character frequency files used to build language-specific profiles[cite: 1].
* **`cache/`**: Serialized JSON frequency maps and intermediate pipeline results[cite: 1].
* **`CLOUS_pipeline.ipynb`**: Main Google Colab notebook containing the complete reproducible evaluation pipeline[cite: 1].
* **`results/`**: Final outputs, including `Figure_1_CLOUS_Heatmap.png`, `Figure_2_Stratified_Scatter.png`, and `Table_3_Djibouti_Effect.csv`[cite: 1].

## Usage
To reproduce the findings or calculate CLOUS scores for new entities:
1. Open `CLOUS_pipeline.ipynb` in Google Colab or your local Jupyter environment.
2. Ensure the `raw_corpora/` and `cache/` directories are accessible in your working directory.
3. Run the cells sequentially to compute character frequency profiles, calculate CLOUS scores, and generate the final correlation benchmarks.

## Citation
If you use CLOUS in your research, please cite the associated paper:

```bibtex
@article{rivera2026clous,
  title={Predicting Cross-Lingual Tokenization Fragmentation: A Frequency-Based Uniqueness Score for Geographic Entities},
  author={Rivera, Richard},
  year={2026},
  note={Independent Research}
}
