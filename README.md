# CLOUS: Cross-Linguistic Orthographic Uniqueness Score

[![Hugging Face Spaces](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/spaces/ric-rivera/CLOUS-Tokenizer-Diagnostic)

Official codebase for the paper: *Estimating Cross-Lingual Tokenization Fragmentation Risk: A Frequency-Based Uniqueness Score for Geographic Entities*.

## Overview

Subword tokenizers distribute vocabulary coverage unevenly across languages and scripts, concentrating entries on character sequences that are frequent in training corpora. Geographic proper nouns are a reproducible stress case for this distributional asymmetry.

This repository introduces the Cross-Linguistic Orthographic Uniqueness Score (CLOUS), a character-level metric based on Shannon surprisal that quantifies the orthographic rarity of localized country names. Evaluated against six production tokenizers across eleven languages, CLOUS shows significant associative strength with tokenization fertility, outperforming naive length-based baselines. 

CLOUS serves as a lightweight pre-tokenization diagnostic for multilingual NLP pipelines, outperforming both naive length-based baselines and a character bigram surprisal baseline in 72% of language-tokenizer combinations. As a high-risk entity screening tool, CLOUS achieves ROC-AUC = 0.850 and F1 = 0.741, correctly identifying approximately three-quarters of the highest-fragmentation entities from orthographic properties alone without model inference.

## 🚀 Live Diagnostic Tool

Test your own geographic entities and visualize tokenization risk across six major models (GPT-4, GPT-4o, Llama 3, Gemma, mBERT, XLM-R) using our interactive web application:
**[CLOUS Tokenizer Diagnostic on Hugging Face](https://huggingface.co/spaces/ric-rivera/CLOUS-Tokenizer-Diagnostic)**

## 📊 Case Study: The Typographical Tax

The fragility of subword tokenizers is highly visible when evaluating subtle stylistic variations in non-Latin scripts. For example, the baseline Arabic entity for Córdoba (`قرطبة`) yields an efficient 3 tokens in GPT-4. However, adding standard typographical elongation lines (`قـــرطـــبـــة`) forces a severe byte-fallback cycle, exploding a 14-character string into **23 separate tokens**. CLOUS accurately flags this structural collapse prior to execution.

## Repository Structure

The project is organized as follows:
* `raw_corpora/`: Leipzig Corpora Collection character frequency files used to build language-specific profiles.
* `cache/`: Serialized JSON frequency maps and intermediate pipeline results (`benchmark_results.csv`, `final_stats.csv`, and `clous_scores.csv`).
* `CLOUS_pipeline.ipynb`: Main Google Colab notebook containing the complete reproducible evaluation pipeline.
* `results/`: Final outputs, including `Figure_1_CLOUS_Heatmap.png` and `Figure_2_Stratified_Scatter.png`.

## Usage

To reproduce the findings or calculate CLOUS scores for new entities: 

1. Download the required Leipzig Corpora Collection character frequency files from [Wortschatz Leipzig](https://wortschatz.uni-leipzig.de/en/download) and place them in the `raw_corpora/` directory. Required files: `en_letters.txt`, `es_letters.txt`, `fr_letters.txt`, `ru_letters.txt`, `ar_letters.txt`, `hi_letters.txt`, `zh-Hans_letters.txt`, `ja_letters.txt`, `ta_letters.txt`, `tr_letters.txt`, `ko_letters.txt`.
2. Open `CLOUS_pipeline.ipynb` in Google Colab or your local Jupyter environment.
3. Ensure the `raw_corpora/` and `cache/` directories are accessible in your working directory.
4. Run the cells sequentially to compute character frequency profiles, calculate CLOUS scores, and generate the final correlation benchmarks.

## Citation

If you use CLOUS in your research, please cite the associated paper:
```bibtex
@article{rivera2026clous,
  title={Estimating Cross-Lingual Tokenization Fragmentation Risk: A Frequency-Based Uniqueness Score for Geographic Entities},
  author={Rivera, Richard},
  year={2026},
  note={Independent Research}
}
